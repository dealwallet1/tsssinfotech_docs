# Odoo 19 Time Off Insights Module - Insights Report, Compensatory Leave Rules & Reminder Email

---

## 1. Overview

The **Odoo 19 Time Off Module** was enhanced with a **Time Off Insights Report**, a **Compensatory Leave workflow with Compensatory Work Date rules**, and an **automatic Reminder Email** to provide a controlled and transparent leave workflow.

The implementation allows HR to see every leave with its balance in one report. For compensatory leave, the employee takes the leave first and must select a valid compensatory work day. The system validates the work date, and reminds the employee and the reporting manager by email before the compensatory work day. The workflow also handles public holidays, Sundays, duplicate work dates, email header errors, and automatic sending through approval and a scheduled job.

---

## 2. Objective

The main objectives of this implementation are:

* Give HR one report to view all leaves with Allocated, Taken, Planned and Remaining days.
* Allow filtering the report by date range, status and leave type.
* Allow a Time Off Type to be marked as a compensatory leave.
* Require a Compensatory Work Date for compensatory leaves.
* Allow the work date only after the leave date.
* Allow the work date only on a Sunday or a Public Holiday.
* Prevent the same work date from being used twice by one employee.
* Show a clear popup message when a wrong work date is selected.
* Send a reminder email to the employee and the reporting manager before the work day.
* Send the reminder automatically, without running any scheduled action manually.
* Keep the existing leave request, allocation and approval functionality separate from this flow.

---

## 3. Requirement

The requirement was to improve the Odoo Time Off module with three features:

1. **Time Off Insights Report** – show all leaves with their balances and filters.
2. **Compensatory Leave with Work Date Rules** – make sure the employee works on a valid compensatory work day after taking the leave.
3. **Compensatory Reminder Email** – remind the employee before the compensatory work day.

---

## 4. Time Off Insights Report

A new report was added under **Time Off > Reporting > Time Off Insights**, visible to Time Off Managers only.

### Information Shown

```text
Employee
Department
Job
Manager
Time Off Type
Applied Date
Start Date / End Date
Days
Status
Applied By
Approved By
Allocated / Taken / Planned / Remaining
```

### Views and Filters

```text
List view
Pivot view
Graph view

Filters:
Approved | Pending | Refused | Cancelled | Compensatory
```

### Date Range

A **Date Range** button was added to the list with the options:

```text
All
Today
This Month
This Quarter
This Year
Custom Range
```

Clicking a row opens the real leave request in a dialog.

---

## 5. Balance Calculation

The balances are calculated by the report itself each time it is opened.

### Workflow

```text
Open Time Off Insights
          ↓
Read approved allocations
          ↓
Read approved leaves
          ↓
Read leaves waiting for approval
          ↓
Calculate balances per employee and leave type
          ↓
Show Allocated, Taken, Planned, Remaining
```

### Formula

```text
Allocated = approved allocations
Taken     = approved leave days
Planned   = leave days waiting for approval
Remaining = Allocated - Taken - Planned
```

### Example

```text
Leave type: Sick Time Off
Allocated: 12 days
Approved leave: 1 day
```

**Result:** Allocated 12, Taken 1, Planned 0, Remaining 11.

Each leave type has its own balance, so taking Sick Time Off does not reduce Paid Time Off.

---

## 6. Compensatory Leave Configuration

First, a new configuration was added at the **Time Off Type** level.

### Field

```text
Is Compensatory Leave
```

When this option is ticked, the leave form of that type shows the **Compensatory Work Date** field and it becomes required.

### Workflow

```text
Administrator
      ↓
Time Off Type
      ↓
Tick "Is Compensatory Leave"
      ↓
Leave form shows Compensatory Work Date
```

The purpose of the field is to record the day on which the employee will work to make up for the leave. The employee takes the compensatory leave first and works on the Compensatory Work Date afterwards.

A **Compensatory Leave Report** under Time Off > Reporting lists the employee, the compensatory date and the work date.

---

## 7. Compensatory Work Date Validation

The leave request was modified to validate the selected work date before saving.

### Rules

```text
1. The work date must be after the leave end date.
2. The work date must be a Sunday or a Public Holiday.
3. One work date can be used only once per employee.
```

### Workflow

```text
Employee selects Compensatory Work Date
                  ↓
        After the leave end date?
             /            \
           No              Yes
           ↓                ↓
    Show popup      Sunday or Public Holiday?
                         /            \
                       No              Yes
                       ↓                ↓
                Show popup      Already used by another leave?
                                     /            \
                                   Yes             No
                                   ↓                ↓
                            Show popup        Accept the date
```

### Example

If the leave is on:

```text
06-11-2026 (Friday)
```

and the employee selects the work date:

```text
08-11-2026 (Sunday)
```

the date is accepted.

If the employee selects:

```text
07-11-2026 (Saturday)
```

the date is blocked, because it is not a Sunday or a Public Holiday.

---

## 8. Sunday and Public Holiday Handling

The work date check uses two sources:

```text
Sunday
   ↓
Accepted directly

Public Holiday
   ↓
Read from Time Off > Configuration > Public Holidays
   ↓
Holiday of the employee's company
   ↓
Holiday for all schedules, or the employee's working schedule
   ↓
Accepted
```

The holiday dates are compared using the **employee timezone**, with the user timezone and UTC as fallback. This prevents incorrect results caused by comparing UTC dates directly with local holiday dates.

Refused and cancelled leaves are ignored in the duplicate check, so their work date becomes available again.

---

## 9. Wrong Date Popup

When the employee selects a wrong work date, an instant popup is shown instead of the generic "Validation Error" dialog.

### Workflow

```text
Employee selects wrong work date
              ↓
Rules are checked immediately
              ↓
Popup: "Compensatory Work Date Not Allowed"
              ↓
Clear message shows the reason
              ↓
Work date field is cleared
              ↓
Employee selects a correct date
```

The same rules are checked again when the leave is saved or approved, as a safety net for imports and code.

### Messages

```text
Work date on or before the leave
→ must be after the leave

Not a Sunday or Public Holiday
→ only a Sunday or a Public Holiday is allowed

Date already used
→ already linked to another compensatory leave
```

---

## 10. Reminder Email Requirement

The third requirement was to send an email to the employee before the compensatory work day.

The system first checks whether the leave is eligible.

### Conditions

```text
Leave is compensatory
        ↓
Leave is approved
        ↓
Reminder status is Pending
        ↓
Work date is today or tomorrow
        ↓
Send reminder
```

### Recipients

```text
Employee work email
        +
Reporting manager work email
        ↓
Empty and duplicate emails removed
```

If neither email exists, no email is sent and the leave stays Pending.

---

## 11. Automatic Sending

The reminder is sent automatically in two ways, so no scheduled action has to be run manually.

### On Approval

```text
Manager approves compensatory leave
              ↓
Work date today or tomorrow?
         /            \
       Yes             No
        ↓               ↓
  Send email now   Wait for scheduled job
```

### Scheduled Job

```text
Scheduled action runs every 1 hour
              ↓
Find approved compensatory leaves
              ↓
Reminder Pending and work date today or tomorrow
              ↓
Send reminder
```

### Example

```text
Leave approved on: 04-11-2026
Work date: 08-11-2026
```

**Result:** The email is not sent on the 4th. The scheduled job sends it on 07-11-2026, the day before the work date.

---

## 12. Reminder Status and Retry

Two fields were added on the leave request:

```text
Work Date Reminder Status  →  Pending / Sent
Work Date Reminder Sent On →  date and time
```

### Workflow

```text
Send reminder
      ↓
Mail delivered?
   /        \
 Yes         No
  ↓           ↓
Status =    Stays Pending
Sent        ↓
            Retried on next run
```

The reminder is marked **Sent** only after the email is really delivered. Changing the work date resets the status to Pending. A sending problem never blocks the approval of the leave.

---

## 13. Email Subject Fix

The reminder emails first failed with the error:

```text
Header values may not contain linefeed or carriage return characters
```

The Subject and From values were saved with line breaks, because the template values were written over several lines.

### Fix

```text
Template values written on one line
              +
Mail header cleaner on every email
              ↓
Line breaks removed from
Subject, From, To, Cc and Reply-To
              ↓
Email is delivered
```

This prevents the error even if a template is edited incorrectly later.

---

## 14. Reminder Email Content

The email explains both the leave date and the compensatory work date, so the employee understands what to do. Dates use the dd-mm-yyyy format.

### Subject

```text
Reminder: Your Compensatory Work Day is tomorrow
```

(The word changes to "today" when the work date is today.)

### Body

```text
Hello Name,

You have taken a compensatory leave on 06-11-2026. For this leave, you will
work on your compensatory work day on 08-11-2026.

So tomorrow is your compensatory work day. Please remember.

Employee:                Name
Leave Type:              Compensatory Days
Leave Date:              06-11-2026
Compensatory Work Date:  08-11-2026
```

---

## 15. Complete Overall Workflow

The complete implementation works like this:

```text
                    EMPLOYEE
                       │
                       ↓
        Applies Compensatory Leave
                       │
                       ↓
        Selects Compensatory Work Date
                       │
              ┌────────┴────────┐
              │                 │
         Date Not Valid      Date Valid
              │                 │
              ↓                 ↓
       Popup Message       Leave Saved
                                │
                                ↓
                       Status: To Approve
                                │
                                ↓
                            MANAGER
                                │
                                ↓
                         Approves Leave
                                │
                                ↓
                  Work date today or tomorrow?
                       ┌────────┴────────┐
                       │                 │
                      Yes               No
                       │                 │
                       ↓                 ↓
              Send Reminder Now    Scheduled Job (hourly)
                       │                 │
                       │          Day before work date
                       │                 │
                       └────────┬────────┘
                                ↓
                  Email to Employee and Manager
                                ↓
                  Reminder Status = Sent
                                ↓
              Visible in Time Off Insights and
                Compensatory Leave Report
```

---

## 16. Example Testing

### Test Case 1 — Balance calculation

```text
Leave type: Sick Time Off
Allocated: 12 days
Approved leave: 1 day
```

**Result:** Remaining is 11 days in the Time Off Insights report.

### Test Case 2 — Work date inside the leave

```text
Leave date: 06-11-2026
Work date: 06-11-2026
```

**Result:** Popup is displayed and the work date is blocked.

### Test Case 3 — Work date on a Saturday

```text
Leave date: 06-11-2026
Work date: 07-11-2026 (Saturday)
```

**Result:** Popup is displayed, because only a Sunday or a Public Holiday is allowed.

### Test Case 4 — Work date on a Sunday

```text
Leave date: 06-11-2026
Work date: 08-11-2026 (Sunday)
```

**Result:** Work date is accepted and the leave is saved.

### Test Case 5 — Work date used twice

```text
Employee: Name
Work date: 08-11-2026 already used by another leave
```

**Result:** Popup is displayed. If the first leave is refused, the date can be used again.

### Test Case 6 — Approval with work date tomorrow

```text
Approval date: 07-11-2026
Work date: 08-11-2026
```

**Result:** Reminder email is sent immediately when the manager approves.

### Test Case 7 — Approval with a later work date

```text
Approval date: 04-11-2026
Work date: 08-11-2026
```

**Result:** Email is sent automatically by the scheduled job on 07-11-2026.

### Test Case 8 — Employee without work email

```text
Employee work email: empty
Manager work email: empty
```

**Result:** No error. Reminder stays Pending.

### Test Case 9 — Normal leave

```text
Time Off Type: Sick Time Off
```

**Result:** No work date is required and no reminder email is sent.

---

## 17. Final Result

The implementation provides a controlled leave workflow where HR can **view all leaves and balances in one report**, employees are **required to select a valid compensatory work date**, and employees and reporting managers receive an **automatic reminder email** before the compensatory work day.

The existing leave request, allocation and approval functionality remains separate from this report, work date and reminder flow.
