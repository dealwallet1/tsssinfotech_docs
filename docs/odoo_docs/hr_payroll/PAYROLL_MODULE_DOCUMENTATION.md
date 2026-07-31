# TDS Payroll Management — Functional Documentation

Module: `employee_tds_management`
Scope: Indian payroll — employee master data, CTC-based salary structuring, statutory deductions (PF, Professional Tax), income tax (TDS) computation, and payslip generation.

This document describes what is actually implemented in the module today (verified against the model code), not aspirational features. Planned/not-yet-implemented items are called out explicitly in [Section 8](#8-known-gaps--not-yet-implemented).

---

## 1. Overview

The module maintains one record per **employee per payroll month** (model `tds.employees`), keyed by `employee_id` + `month` + `financial_year_id`. Each record captures the employee's master data for that month, their input Annual CTC, and a full chain of computed fields (salary breakup → PF → Professional Tax → TDS → net pay), so every payslip is self-contained and auditable.

Supporting models:

| Model | Purpose |
|---|---|
| `tds.employees` | Employee master + monthly payroll record (core model) |
| `tds.companies` | Company/legal entity: PF policy, PAN/TAN/GSTIN, address, fiscal year start |
| `tds.financial.year` | Financial year master (start/end dates) |
| `pf.config` | Per-company PF employee/employer contribution rates — **defined but not actually used**, see §4.1 and §8 |
| `pt.service` | Stateless service that computes Professional Tax by employee state |
| `tds.employee.dashboard` | Transient model powering the employee self-service landing page |
| `tds.private.key.wizard` | Admin wizard to unlock a locked (encrypted) employee record |
| `tds.payslip.download.wizard` | Wizard to download a single month's payslip (3/6-month bundling exists in code but isn't wired to any UI — see §8) |

---

## 2. Employee Master Data

All fields below live on `tds.employees` (`models/tds_employee.py`).

### 2.1 Basic Information

| Field | Type | Notes |
|---|---|---|
| `name` | Char | Employee name, required |
| `employee_id` | Char | Employee ID/code, required, indexed |
| `designation` | Char | Required |
| `date_of_joining` | Date | Required |
| `email` | Char (encrypted) | Also used to derive one of the two wrapped copies of the employee's AES data key |
| `department_id` | Char | Free-text department (not a relation to `hr.department`) |
| `state_id` | Many2one → `res.country.state` | Required; drives Professional Tax slab |

### 2.2 Statutory Details

| Field | Type | Notes |
|---|---|---|
| `pan_number` | Char (encrypted, masked) | Shows only first 2 + last 4 characters unless the record is unlocked |
| `uan_number` | Char (encrypted, masked) | Universal Account Number (EPFO) |
| `pf_account_number` | Char (encrypted) | |
| `esic_account_number` | Char (encrypted) | ESIC account number is **stored** but see [§8](#8-known-gaps--not-yet-implemented) — there is no automatic ESI eligibility check or ESI contribution computation yet |

### 2.3 PF & ESI Eligibility

- `pf_applicable` (Boolean, default `True`) — a manual toggle per employee. When off, `pf_employee` and `pf_employer` are forced to 0. There is currently **no automatic eligibility rule** (e.g. based on Basic salary crossing ₹15,000/₹21,000 thresholds); it is set by the HR user.
- There is **no equivalent `esi_applicable` field** — ESI is not yet part of the computation engine (account number only).

### 2.4 Bank Details

| Field | Type |
|---|---|
| `payment_mode` | Selection: Bank Transfer / Cash / Cheque |
| `bank_name`, `branch_name`, `ifsc_code` | Char (encrypted) |
| `bank_account_number` | Char (encrypted, masked) |

### 2.5 Payroll Context

| Field | Notes |
|---|---|
| `company_id` | Many2one → `tds.companies`, required |
| `financial_year_id` | Many2one → `tds.financial.year`, required |
| `month` | Selection 01–12, required — the payroll month this record represents |
| `tax_regime` | Selection: Old / New, required — drives the entire TDS calculation |
| `login_username` / `login_password` | Declared but **unused** — not read/written anywhere else in the module and not present on the form view; actual self-service login is the employee's real Odoo login matching `employee_id` (§7, §9), not these fields |

### 2.6 Leave Without Pay (LWP)

| Field | Notes |
|---|---|
| `working_days` | Default 30 |
| `lwp_days` | Days of unpaid leave in the month |
| `lwp_amount` (computed) | `(gross_salary / working_days) * lwp_days` |

---

## 3. CTC-Based Salary Structure

The module follows a **single-source-of-truth CTC model**: HR enters one number, `annual_ctc_input`, and every other salary component is derived from it automatically.

### 3.1 Computation Chain

```
annual_ctc_input  (HR input, per financial year)
        │  ÷ 12
        ▼
monthly_ctc
        │
        ├── base_salary        = monthly_ctc × 40%
        │        └── hra       = base_salary × 50%
        ├── lta                = monthly_ctc × 2%
        ├── medical_allowance  = monthly_ctc × 1%
        │
        ▼
   pf_employer  (computed from base_salary, see §4.1)
        │
        ▼
monthly_salary = monthly_ctc − pf_employer      (employee-facing CTC, i.e. CTC minus employer's PF)
        │
        ▼
special_allowance = monthly_salary − (base_salary + hra + lta + medical_allowance)   ← balancing figure
        │
        ▼
gross_salary = base_salary + hra + lta + medical_allowance + special_allowance
```

> **Correctness risk — circular `@api.depends` graph.** `base_salary`/`special_allowance` (`_compute_salary_breakup`) depend on `monthly_salary`; `monthly_salary` (`_compute_monthly_salary`) depends on `pf_employer`; `pf_employer` (`_compute_pf`) depends on `base_salary` — a cycle: `base_salary → monthly_salary → pf_employer → base_salary`. It doesn't currently loop infinitely or blow up only because `_compute_salary_breakup` happens to assign `rec.base_salary` *before* it reads `rec.monthly_salary` a few lines later in the same loop body — Odoo's lazy field access then resolves the nested `monthly_salary → pf_employer → base_salary` chain using the value just assigned, instead of a stale/zero one. That's incidental to statement order, not a guarantee: reordering those lines, splitting the method, or a future Odoo version's recompute batching could silently reintroduce stale values (e.g. `special_allowance`/`gross_salary` computed off a zero `monthly_salary` on first save) with no error raised. Worth breaking the cycle deliberately (e.g. compute PF off `annual_ctc_input`/`monthly_ctc` directly instead of the post-breakup `base_salary`) rather than relying on this ordering.

### 3.2 Salary Components (Monthly)

| Component | Formula | Field |
|---|---|---|
| Basic Salary | 40% of Monthly CTC | `base_salary` |
| HRA | 50% of Basic Salary | `hra` |
| Leave Travel Allowance (LTA) | 2% of Monthly CTC | `lta` |
| Medical Allowance | 1% of Monthly CTC | `medical_allowance` |
| Special Allowance | Balancing figure (Monthly Salary − Basic − HRA − LTA − Medical) | `special_allowance` |
| **Gross Salary** | Sum of all the above | `gross_salary` |

### 3.3 CTC Reconciliation

| Field | Formula |
|---|---|
| `ctc` (monthly, recomputed) | `gross_salary + pf_employer` |
| `annual_ctc` | `annual_salary + annual_pf_employer` (annual_salary = `gross_salary × 12`) |

This lets HR verify that the CTC actually paid out (gross + employer PF, annualized) reconciles back to the `annual_ctc_input` they originally entered.

---

## 4. Statutory Deductions

### 4.1 Provident Fund (PF)

Computed in `_compute_pf`, driven by per-company policy fields declared directly on **`tds.companies`**:

- `pf_cap_applicable` (company setting, default on) — if enabled, PF is calculated on Basic salary **capped at ₹15,000** (the statutory EPFO wage ceiling); if disabled, PF is calculated on full Basic salary.
- `pf_employee_rate`, `pf_employer_rate` — per-company percentage, default **12%** each.
- If `pf_applicable` is unchecked on the employee, both `pf_employee` and `pf_employer` are forced to 0.

> **Note:** there is a separate `pf.config` model (`models/pf_config.py`) that also defines `employee_rate` / `employer_rate` per company, but it is not read by `_compute_pf` (or anywhere else) and has **no entry in `security/ir.model.access.csv`**, so no non-superuser can even open it — it's an orphaned model, not a second source of truth. The rates that actually apply are the ones on the `tds.companies` form.
>
> **Note:** `pf_employee_rate` and `pf_employer_rate` are, in turn, not actually exposed on the `tds.companies` form view (`views/tds_company.xml`) — only `pf_cap_applicable` is shown under "Statutory Details". So in normal UI use, every company is effectively locked to the Python-level default of **12% / 12%**; changing the rate per company requires editing the record through Odoo's technical/developer UI rather than the module's own Company screen.

```
pf_base      = min(base_salary, 15000)   if pf_cap_applicable else base_salary
pf_employee  = pf_base × pf_employee_rate / 100
pf_employer  = pf_base × pf_employer_rate / 100
```

Annual figures (`annual_pf_employee`, `annual_pf_employer`) are simply the monthly figures × 12.

### 4.2 Professional Tax (PT)

Computed by the stateless `pt.service` model (`models/professional_tax.py`), based on the employee's `state_id` and monthly `gross_salary`:

- **Flat ₹200/month** states: Andhra Pradesh, Telangana, Gujarat, Madhya Pradesh, Kerala, Assam, Bihar, Odisha.
- **Slab-based** states:
  - **Maharashtra**: ₹0 up to ₹7,500 → ₹175 up to ₹10,000 → ₹200/month (₹300 in February) above that.
  - **Karnataka**: ₹0 up to ₹15,000 → ₹150 up to ₹25,000 → ₹200 above.
  - **Tamil Nadu**: ₹0 / ₹135 / ₹315 / ₹690 / ₹1,025 across ₹21,000–₹60,000+ salary bands.
  - **West Bengal**: ₹0 / ₹110 / ₹130 / ₹200 across ₹10,000–₹25,000+ bands.
- All other states: ₹0 (not configured).

> **Bug:** the Maharashtra February bump (₹300 instead of ₹200) is decided by `fields.Date.today().month` inside `_compute_pt` — i.e. the **real-world calendar month at the moment the record is (re)computed** — not by the payslip's own `month` field. So a Maharashtra payslip for, say, February is only charged ₹300 if it happens to be computed/saved *during* February; recomputing it in any other month recalculates it back down to ₹200, and conversely every Maharashtra payslip touched during February (regardless of which payroll month it's actually for) briefly gets the ₹300 rate. `emp.month` (the payslip's own selection field) is available but unused here.

### 4.3 ESI

Not yet computed automatically — see [§8](#8-known-gaps--not-yet-implemented).

---

## 5. Income Tax (TDS) Engine

TDS is recomputed on every save from `gross_salary`, `tax_regime`, and (for the Old Regime) the employee's declared deductions. `annual_income = gross_salary × 12`. A ₹50,000 **Standard Deduction** applies in both regimes.

### 5.1 New Tax Regime (Section 115BAC) — default

1. `taxable = annual_income − 50,000` (floored at 0)
2. **Section 87A rebate**: if `taxable ≤ ₹12,00,000`, tax = 0
3. Otherwise, slab computation:

| Taxable Income Slab | Rate |
|---|---|
| ₹0 – ₹4,00,000 | 0% |
| ₹4,00,000 – ₹8,00,000 | 5% |
| ₹8,00,000 – ₹12,00,000 | 10% |
| ₹12,00,000 – ₹16,00,000 | 15% |
| ₹16,00,000 – ₹20,00,000 | 20% |
| ₹20,00,000 – ₹24,00,000 | 25% |
| Above ₹24,00,000 | 30% |

4. **+4% Health & Education Cess** on the computed tax.

### 5.2 Old Tax Regime

1. Allowed deductions are capped and summed:
   - Section 80C: `min(deduction_80c, ₹1,50,000)`
   - Section 80D: `min(deduction_80d, ₹50,000)`
   - NPS (80CCD(1B)): `min(deduction_nps, ₹50,000)`
   - HRA exemption: `hra_exemption` (as declared, no automatic cap in code)
   - Home Loan Interest (Section 24(b)): `allowed_home_loan_interest` — self-occupied capped at ₹2,00,000; let-out property uncapped (see caveat in §8 — this field and its compute logic are declared twice in the model)
2. `taxable = annual_income − 50,000 (standard deduction) − sum(above deductions)`, floored at 0
3. **Section 87A rebate**: if `taxable ≤ ₹5,00,000`, tax = 0
4. Otherwise, slab computation on `taxable − ₹2,50,000` (basic exemption already carved out):

| Slab (on remaining taxable, after ₹2.5L exemption) | Rate |
|---|---|
| Next ₹2,50,000 (i.e. ₹2.5L–₹5L) | 5% |
| Next ₹5,00,000 (i.e. ₹5L–₹10L) | 20% |
| Balance above ₹10L | 30% |

5. **+4% Health & Education Cess** on the computed tax.

### 5.3 Outputs

| Field | Meaning |
|---|---|
| `annual_salary` | `gross_salary × 12` |
| `annual_tds` | Computed annual tax (rounded to 2 decimals) |
| `monthly_tds` | `annual_tds / 12` |

Deduction input fields (`deduction_80c`, `deduction_80d`, `deduction_nps`, `home_loan_interest`, `hra_exemption`) and their "allowed" counterparts are only meaningful — and only shown in the form — when `tax_regime = 'old'`; under the New Regime the allowed-deduction fields are force-zeroed.

---

## 6. Net Salary & Totals

```
net_salary        = gross_salary − pf_employee − pt_amount − monthly_tds − lwp_amount
annual_net_salary = annual_salary − (annual_pf_employee + annual_pt_amount)
```

`other_deductions` exists as a manual input field but is **not currently wired into** `net_salary` — see [§8](#8-known-gaps--not-yet-implemented).

`annual_pt_amount` in the `annual_net_salary` formula above is, in practice, always **0** — its compute method never actually assigns it a value (see [§8](#8-known-gaps--not-yet-implemented)), so `annual_net_salary` effectively reduces to `annual_salary − annual_pf_employee` only, silently never accounting for annual Professional Tax.

---

## 7. Payslips, Reports & Employee Self-Service

- **Payslip PDF** (`action_print_payslip`, template `reports/tds_payslip_with_form16_template.xml`, action defined in `reports/payslip_report.xml`) shows: employee details (Name, Designation, Employee ID, Date of Joining, UAN, PAN, Bank A/C No., IFSC, Paid Days, LWP Days), then an Earnings vs. Deductions table (Basic, HRA, LTA, Medical, Special Allowance vs. PF, TDS, Professional Tax, Other Deductions), Total Earnings, Total Deductions, and Net Salary Payable.
- **Single month/year download wizard** (`tds.payslip.download.wizard`) — the only download path actually wired to the UI (the "Download Payslip" button on the employee form). The user picks a Year (current year and up to 5 years back, never a future year) and Month; the wizard resolves the matching `tds.financial.year` and looks up the one payslip record for that employee/month, then streams the PDF directly (`config=False` skips Odoo's one-time "configure document layout" prompt).
- **Employee Self-Service Dashboard** (`tds.employee.dashboard`) — a non-admin user logging in with a 4-digit numeric login (matched against `employee_id`) is routed straight to their own payroll record in read view. Admins instead see a notice pointing them to the standard management views. The login page itself is relabelled "Employee Id" instead of the default Odoo login (`views/login_templates.xml`).

---

## 8. Known Gaps / Not Yet Implemented / Dead Code

These are visible in the code as stored-but-unused fields, orphaned compute methods, commented-out logic, report/logic mismatches, or items called out in the module README's "Planned Future Enhancements" that never made it into the code:

- **ESI is not computed.** `esic_account_number` is stored, but there is no `esi_applicable` eligibility flag and no `esi_employee` / `esi_employer` contribution computation anywhere in the active code (only present in a commented-out draft of `action_send_payslip_email`), and ESI never appears on the payslip.
- **`other_deductions` is inconsistent between net pay and the payslip.** It is **not** subtracted in `_compute_net` (`net_salary` = gross − PF − PT − TDS − LWP only), but the payslip PDF's printed "Total Deductions" figure **does** include it (`pf_employee + monthly_tds + pt_amount + other_deductions` — note PT, not ESI, is being added here). Net effect: on a payslip where `other_deductions > 0`, the printed "Total Deductions" and "Net Salary Payable" rows won't reconcile (Total Earnings − Total Deductions ≠ Net Salary Payable).
- **Payslip PDF has a duplicated "Professional Tax" row.** The deductions column lists "Professional Tax" twice (once opposite LTA, once opposite Medical Allowance, both showing `pt_amount`) instead of a second, distinct line — most likely a copy/paste leftover from where an ESI row was probably intended.
- **"Form 16–style tax summary" and "Net Salary in words" are not actually in the report**, despite being claimed in `README.md` and the filename `tds_payslip_with_form16_template.xml`. The template only renders the employee-details block and the earnings/deductions table above — there is no annual tax breakup or Form 16 section, and `net_salary_in_words` is never referenced by it.
- **`_compute_net_in_words` / `net_salary_in_words` is orphaned code.** The field `net_salary_in_words` is never declared on the model (no `fields.Char(compute="_compute_net_in_words")`), so this method is never invoked by the ORM and nothing ever calls it manually either — the `num2words` Indian-format conversion described in the README is not actually wired up anywhere.
- **`_compute_age` is orphaned code** for the same reason: it references `date_of_birth` and sets `age`, but neither field is declared on `tds.employees`, so there is no age field or date-of-birth capture anywhere in the module, and this method never runs.
- **`employee_encrypted_email` is write-only.** It's generated and stored at `create()` (an email-derived AES-key wrapping, intended as a secondary/recovery unwrap path per the code comments) but no code anywhere reads it back or decrypts with it — there is no email-based recovery flow implemented, only the RSA-based one.
- **3/6-month payslip bundling is unreachable from the UI.** `action_download_3_months`, `action_download_6_months`, `_get_period_payslips`, `duration_months`, and `month_range` all exist on `tds.employees`, but no view, button, or menu references them — only the single month/year wizard (§7) is actually exposed to users.
- **Professional Tax's Maharashtra February surcharge is keyed off today's date, not the payslip's month** — see the callout in §4.2. This means the ₹300-vs-₹200 rate can be wrong for any Maharashtra payslip that isn't (re)computed during the actual month of February.
- **`annual_pt_amount` is declared as a stored, computed field (`compute="_compute_annual_totals"`) but that method never assigns it.** It silently stays at 0.0, and — because the same method reads `rec.annual_pt_amount` while deriving `annual_net_salary` — annual Professional Tax is never actually subtracted from `annual_net_salary` (see §6).
- **`_compute_annual_totals`'s `@api.depends` is incomplete.** It only declares `('gross_salary', 'pf_employer')`, but the method body also reads `rec.pf_employee` and `rec.annual_pt_amount`. In practice `pf_employee` still recomputes correctly because it shares the same upstream triggers as `pf_employer` (both come from `_compute_pf`), but the missing dependency is fragile and, combined with the point above, means PT changes never trigger a recompute of `annual_net_salary` at all.
- **`annual_salary` is computed by two different methods.** The field declares `compute="_compute_tds"`, but `_compute_annual_totals` also independently assigns `rec.annual_salary = rec.gross_salary * 12` (the same formula, so no visible discrepancy today, but it's duplicate logic living in two places that could silently diverge if either is edited later).
- **`home_loan_interest` and `allowed_home_loan_interest` are each declared twice** in `tds_employee.py` (once near the 80C/80D/NPS deduction block, again near the Home Loan / `property_type` block). Python keeps only the second declaration as the live field (the `property_type`-aware one, computed by `_compute_allowed_home_loan_interest`), but the first compute method (`_compute_allowed_deductions`) still runs and still writes its own `min(home_loan_interest, 200000)` value into `allowed_home_loan_interest` — competing with the let-out-uncapped logic in `_compute_allowed_home_loan_interest`. Whichever compute happens to run last on a given recompute wins, so the let-out-property "no cap" behavior isn't guaranteed to stick.
- **`pf.config` is an orphaned model** — defined, imported, but has no access rights (missing from `ir.model.access.csv`) and no menu/view, so it can't be opened by any non-superuser; it also isn't read by the PF computation (see §4.1).
- **`base_salary` ↔ `monthly_salary` ↔ `pf_employer` form a circular `@api.depends` graph** — see the callout in §3.1. It happens not to misbehave today only because of incidental line ordering inside `_compute_salary_breakup`.
- **`tds.companies`' PF rate fields aren't editable from the Company form.** `pf_employee_rate` / `pf_employer_rate` exist on the model and drive real payroll math (§4.1), but `views/tds_company.xml` only exposes `pf_cap_applicable` — every company is effectively stuck at the 12%/12% default via normal UI use.
- **`currency_id` and `fiscalyear_start_month` on `tds.companies` are declared (with sensible defaults — company currency, April) but never shown on the Company form and never read by any computation.** Financial years are instead created manually with explicit start/end dates via the separate Financial Years menu, so `fiscalyear_start_month` has no effect on anything.
- **No automatic PF/ESI eligibility rule** based on salary thresholds — `pf_applicable` is a manual checkbox, not derived from Basic salary.
- **Payslip email delivery** (`action_send_payslip_email`) is fully written but commented out / disabled in both the model and the form view.
- Per the module README, not yet built: surcharge calculation, marginal relief, state-wise Professional Tax beyond the states listed in §4.2, automatic Old-vs-New regime comparison, Excel export, multi-company consolidated handling, and year-wise (vs. hardcoded FY 2026–27) slab configuration.

---

## 9. Data Security Model

Sensitive employee fields (email, PAN, UAN, bank details, all salary figures, tax deductions) use custom `EncryptedChar` / `EncryptedFloat` field types (`models/encrypted_fields.py`).

### 9.1 Key Generation (per employee, at `create()`)

`generate_employee_keys(email)` in `models/aes_key_manager.py`:

1. `generate_employee_aes_key()` — `os.urandom(32)`, a fresh random **256-bit AES key**, one per employee record (not shared across employees or reused from a prior record).
2. That raw AES key is wrapped two different ways and both wrapped forms are stored on the record:
   - **`employee_data_key`** — the AES key encrypted with the **server's RSA-4096 public key** (`keys/public_key.pem`) using **RSA-OAEP with SHA-256** padding, base64-encoded. This is the one actually used for all normal encrypt/decrypt operations.
   - **`employee_encrypted_email`** — the *same* raw AES key, separately encrypted with **AES-256-GCM** using a key derived as `SHA-256(email.strip().lower())`. Per the code's own comment this is a deliberately weaker wrap (an email isn't a secret), and per §8 it's currently write-only — nothing in the module reads it back to actually recover a key from it.

### 9.2 Field-Level Encrypt/Decrypt Path

`EncryptedChar` and `EncryptedFloat` are Odoo field subclasses that hook into the ORM's read/write conversion pipeline (`convert_to_cache` / `convert_to_column` / `convert_to_record`) so encryption is invisible to the rest of the model — compute methods, views, and reports all just see plaintext Python values:

- **In memory (cache):** always plaintext. `convert_to_cache` never encrypts, so onchange handlers and compute chains (e.g. the whole salary-breakup/PF/TDS chain in §3–§6) never pay a decrypt cost mid-computation.
- **On write (`convert_to_column`, i.e. the value actually going to Postgres):** the AES key is resolved (see below), then the plaintext is encrypted with **AES-256-GCM** using a fresh random **12-byte nonce** per write (`os.urandom(12)`). The stored column value is `"AESENC::" + base64(nonce + ciphertext)` — the `AESENC::` marker lets the code tell encrypted values apart from any legacy/plain value that might exist without needing a separate schema flag.
- **On read (`convert_to_record`, i.e. loading the column value back into a record):** if the marker is present, the payload is base64-decoded, split back into `nonce` (first 12 bytes) and `ciphertext` (remainder), and decrypted with AES-GCM using the resolved key; GCM's built-in authentication tag means any tampering with the stored ciphertext fails decryption outright rather than returning corrupted plaintext.
- **Resolving the AES key** for a given record: `employee_data_key` is RSA-OAEP-decrypted using the **server's private key file** (`decrypt_with_server_private_key`, reading `keys/private_key.pem`). This RSA decrypt is wrapped in an `lru_cache(maxsize=1024)` keyed on the ciphertext itself, so repeatedly rendering the same record's fields (e.g. across several fields on one form) only pays the RSA-4096 decrypt cost once.
- If no data key is available yet for a brand-new, unsaved record, `EncryptedChar`/`EncryptedFloat` fall back to leaving the value as plaintext for that flush — it gets encrypted on the next write once `create()` has assigned `employee_data_key`.

### 9.3 Masking vs. Encryption (two separate mechanisms)

Encryption (§9.2) and masking are independent layers:

- **Encryption** governs what's in the database column, and is transparent to any code path with ORM read access to the record — encryption alone does not hide a field's value from an authenticated user browsing the form.
- **Masking** is the actual "hide it from casual view" mechanism, and only applies to `PAN`, `UAN`, and `bank_account_number` (`EncryptedChar(..., mask=True)`). After decryption, `convert_to_record` additionally checks `record._is_unlocked()`; if the record isn't unlocked, only the first 2 and last 4 characters are returned (e.g. `AB******IJKL`) instead of the full decrypted value.
- **Encryption at rest protects the raw database column, not app-level reads.** For ordinary list/form views, dashboard access, and payslip generation, non-masked encrypted fields are decrypted transparently using the server's own private key file — any user with model read access (see row-level rule below) sees plaintext values, no unlock step needed. Only the three masked fields require an unlock to see in full.

### 9.4 Record Locking & Access Control

- **Record locking (edit gate, not a read gate)**: once an employee record exists, it opens read-only (`is_locked = True`) for writes, and masked fields stay masked, until a user unlocks it. Unlocking requires an admin (`base.group_system`) to paste the RSA **private key PEM** into `tds.private.key.wizard`; the wizard doesn't use the server's key file for this — it validates the admin-supplied PEM by attempting `decrypt_with_private_key_pem` directly against that employee's `employee_data_key`, i.e. proof that the pasted key can actually unwrap this specific record's AES key. On success it issues a 60-minute unlock cookie (`tds_unlock_token` on `res.users`, HttpOnly, `Secure` when served over HTTPS) scoped to that browser session. Printing/downloading a payslip also implicitly sets `data_unlocked=True` for that request, so masked fields render unmasked on the PDF regardless of the record's lock state.
- **Row-level security** (`security/security.xml`, `ir.rule`): non-admin users (`base.group_user`) can only see `tds.employees` records where `employee_id = user.login` — i.e., their own payroll records only, keyed off their Odoo login matching their employee code. Admins (`base.group_system`) have an unrestricted `(1,'=',1)` rule with full read/write/create/unlink.
- **Menu access reinforces this**: the entire "Payroll" menu tree (Companies, Employees, Financial Years, Configuration — `views/tds_menu.xml`) is restricted to `base.group_system`. Regular employees have no menu path into these list/form views at all; their only entry point is the "My Payroll Dashboard" action (`base.group_user`), which redirects them straight to their own record via `tds.employee.dashboard` (§7) — the row-level rule above is what stops them from then browsing to anyone else's record by URL/ID.
- **Model-level access** (`security/ir.model.access.csv`): regular users get read/write but not create/unlink on employee, company, and financial year records (the row-level rule above further restricts *which* employee rows that applies to); only `base.group_system` (admins) can create or delete them.
- **⚠️ The RSA private key is committed to the git repository** (`keys/private_key.pem`, `keys/public_key.pem` are tracked files, not covered by `.gitignore`, added in commit `82e7451`). This undermines the "admin must supply the private key" unlock control in any environment where the deployed code is a checkout of this repo — anyone with repository access already has the key needed to unlock any record or decrypt the database column ciphertext directly. This should be rotated out of the app's `keys/` directory and generated per-deployment instead (the module already has `rsa_key_manager.generate_rsa_key_pair()` for this, meant to be run once via `odoo-bin shell`).

---

## 10. Module Dependencies

- Odoo modules: `base`, `mail`, `web`
- Python: `cryptography` (AES-GCM + RSA-OAEP), `num2words` (amount-in-words utility — imported but not currently wired into any active output, see §8), `reportlab` (only used by the disabled `action_send_payslip_email` PDF-and-email flow, not by the active QWeb payslip report)
- Target: Odoo 19, Python 3.10+
