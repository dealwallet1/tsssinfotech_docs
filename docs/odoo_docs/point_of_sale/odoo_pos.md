# Odoo Point of Sale Documentation

## Table of Contents
- [IOT Configuration](#iot-configuration)
  - [Pre-requisites](#pre-requisites)
  - [IoT System Setup](#iot-system-setup)
  - [Connecting Peripheral Devices](#connecting-peripheral-devices)
  - [Integrate IoT System with Odoo POS](#integrate-iot-system-with-odoo-pos)
  - [Device Monitoring](#device-monitoring)
  - [ePOS Printers](#epos-printers)
  - [Secure Connection (HTTPS)](#secure-connection-https)
  - [Self-Signed Certificates for ePOS Printers](#self-signed-certificates-for-epos-printers)
- [Multi-Employee Management](#multi-employee-management)
- [Receipts and Invoices](#receipts-and-invoices)
- [Preparation Display](#preparation-display)
- [Self-Ordering](#self-ordering)
- [Product Combos](#product-combos)
- [Shop Features](#shop-features)
  - [Sales Orders](#sales-orders)
  - [Barcodes](#barcodes)
  - [Serial Numbers and Lots](#serial-numbers-and-lots)
  - [Ship Later](#ship-later)
  - [Customer Display](#customer-display)
- [Restaurant Features](#restaurant-features)
  - [Floors and Tables](#floors-and-tables)
  - [Orders Printing](#orders-printing)
  - [Bills](#bills)
  - [Tips](#tips)
- [Pricing Features](#pricing-features)
  - [Discounts](#discounts)
  - [Discount Tags (Barcode Scanner)](#discount-tags-barcode-scanner)
  - [Loyalty Programs](#loyalty-programs)
  - [Pricelists](#pricelists)
  - [Flexible Taxes (Fiscal Positions)](#flexible-taxes-fiscal-positions)
  - [Cash Rounding](#cash-rounding)
  - [Electronic Shelf Labels (Pricer Integration)](#electronic-shelf-labels-pricer-integration)
- [Payment Methods](#payment-methods)
  - [QR Code Payments](#qr-code-payments)
  - [Payment Terminals (Razorpay)](#payment-terminals-razorpay)
- [Marketing Features](#marketing-features)
  - [Email Marketing](#email-marketing)
  - [WhatsApp Marketing](#whatsapp-marketing)
- [UrbanPiper Integration for Online Food Delivery](#urbanpiper-integration-for-online-food-delivery)
- [Reporting](#reporting)

---

## IOT Configuration

### Pre-requisites
- Ensure the **Point of Sale** and **Internet of Things (IoT)** apps are installed.

### IoT System Setup
- **Option A**: Set up an **IoT Box**.
- **Option B**: Use a **Windows virtual IoT environment**.

### Connecting Peripheral Devices
- **Printer**: Connect to USB or network; power on.
- **Cash Drawer**: Connect via RJ25 cable to printer.
- **Barcode Scanner**: Must end barcodes with ENTER (keycode 28).
- **Scale**: Connect and power on.
- **Customer Display**: Connect screen to IoT Box.
- **Payment Terminal**: Follow vendor-specific instructions.

### Integrate IoT System with Odoo POS
1. Go to **POS > Settings**.
2. Edit your POS.
3. In **Connected Devices**, enable **IoT Box** and select devices.
4. Click **Save**.

### Device Monitoring
- View **IoT Devices** to check connection status.
- Click a device for configuration options.

### ePOS Printers

#### Configuration
1. In **POS Settings**, activate **ePOS Printer**.
2. Enter the printer’s **IP address**.
> **Note**: Networked ePOS printers auto-print a ticket with their IP.

#### Directly Supported ePOS Printers (No IoT Required)
- Epson TM-m30 i/ii/iii (Wi-Fi/Ethernet)
- Epson TM-H6000IV-DT
- Epson TM-T70II-DT, TM-T88V-DT, TM-L90-i, TM-T70-i, TM-T82II-i, TM-T83II-i, TM-U220-i
- Epson TM-m10
- Epson TM-P20, TM-P60II, TM-P80 (Wi-Fi models)

#### ePOS Printers Requiring IoT System
- Epson TM-T20, TM-T88, TM-U220 families (USB-only or ESC/POS)

> **Important**:
> - Wi-Fi/Ethernet Epson printers using **EPOS SDK JS** work directly.
> - **ESC/POS** printers require IoT.
> - **Bluetooth printers are not supported**.

### Secure Connection (HTTPS)
If using **Direct Devices** (e.g., ePOS), Odoo defaults to HTTP.

To enforce HTTPS:
1. Enable **Developer Mode**.
2. Go to **Settings > Technical > Parameters > System Parameters**.
3. Create new parameter:
   - **Key**: `point_of_sale.enforce_https`
   - **Value**: `True`
4. Save.

### Self-Signed Certificates for ePOS Printers
Some ePOS printers require HTTPS. Browsers show warnings unless you install a trusted cert.

#### Generate Certificate
1. Visit `https://[printer-ip]`.
2. Force unsafe connection (Advanced > Proceed).
3. Log in:  
   - **ID**: `epson`  
   - **Password**: Printer serial number
4. Go to **Authentication > Certificate List > Create**.
5. Set **Common Name** = printer IP.
6. Set validity period → **Create**.
7. **Restart** printer.
8. Go to **Security > SSL/TLS** → select **Selfsigned Certificate**.

> ⚠️ Only generate **one** certificate. Generating another invalidates the old one.

#### Export & Import Certificate
- Export from printer UI.
- Import into OS/browser trust store.

#### Verify
Visit `https://[printer-ip]` again. Padlock = success.

---

## Multi-Employee Management

### Configuration
1. In **POS Settings > Interface**, enable **Log in with Employees**.
2. Set:
   - **Basic rights**: Standard access employees.
   - **Advanced rights**: Extended permissions.

> - Empty **Basic** = all employees can log in.  
> - Empty **Advanced** = only Odoo users get advanced rights.

### Access Rights (Basic)
- Open/lock sessions
- Cash in/out
- Toggle product/category images
- Process sales, refunds, orders
- Set customers, view history
- Apply pricelists, discounts, fiscal positions

### Usage
- Log in via **badge scan**, **name**, or **PIN**.
- Switch users during session by clicking current name.
- **No scanner?** Use webcam (click barcode icon).

### Badge & PIN Setup
- **Badge ID**: In **Employee > Settings**, under *Attendance/POS/Manufacturing*.
  - Enter or **Generate**, then **Print Badge**.
- **PIN Code**: Set in same section for secure login.
- Lock session (🔒 icon) to allow new user.

---

## Receipts and Invoices

### Receipts
1. Go to **POS > Configuration > Point of Sale**.
2. Under **Bills & Receipts**:
   - Enable **Header & Footer** and fill them.
   - Enable **Automatic Receipt Printing**.
3. To reprint:
   - Click **Orders** → filter **Paid** → select order → **Print Receipt**.
   - Search by receipt #, date, or customer.

### Invoices
- Invoices require a **registered customer**.
- Issuing an invoice posts to accounting journal.

#### Configure Journals
- In **POS Settings > Accounting**, set default journals.

#### Issue Invoice
- During payment, click **Invoice** under customer name.
- Select payment → **Validate**.

#### Retrieve Invoices
- Go to **POS > Orders > Orders** → click order → **Invoice** smart button.
- Filter with **Filters > Invoiced**.

### QR Code for Invoices
- Customers scan QR on receipt to request invoice.
- They fill billing details → invoice generated & downloadable.
- Order status changes to **Invoiced**.

#### Enable QR Code
1. In **POS Settings > Bills & Receipts**.
2. Enable **Use QR code on ticket**.

---

## Preparation Display

### Purpose
- **Retail**: Notify staff to prepare items.
- **Restaurants**: Send orders to kitchen/bar.

### Configuration
1. In **POS > Settings**, enable **Preparation Display**.
2. Go to **POS > Orders > Preparation Display > New**.
   - **Name**: e.g., "Main Kitchen"
   - **Point of Sale**: assign POS
   - **Product Categories**: filter
   - **Stages**: add steps (with colors & timers)

> Use **⋮** on display card to edit.

### Practical Use
- View displays: shows stages, orders, avg prep time.
- **Tip**: Use **Kitchen Display** app icon on dashboard.

### Using the Display
- Click **Preparation Screen**:
  - Stages with order counts
  - Product categories
  - Order cards: table #, status (color), wait time (red if delayed)
  - Click items to mark done; click card to advance stage.
  - Use **Recall** to undo completion.

### Customer Display
- Click **Order Status Screen**:
  - Shows **Ready** and **In Progress** orders.
  - Customers use receipt order # to track.

---

## Self-Ordering

### Configuration

#### Feature Activation
1. In **POS Settings > Mobile self-order & Kiosk**.
2. Choose **Self Ordering type**:
   - QR menu
   - Kiosk
   - QR menu + Ordering
3. Click **Print QR Codes** (PDF) or **Download QR Codes** (ZIP).

> - Restaurants: one QR per table.  
> - Shops: one general QR.

#### Additional Settings
- **Home Buttons**: Add custom links (e.g., promo page).
- **Service Location**: Require table assignment?
- **Payment**: Enable online methods (card, wallet).
- **Language**: Allow language switch.
- **Splash Screens**: Add loading screen.
- **Eat in / Take out**: Enable preference selection.

#### Preview
- Click **Preview Web Interface** to test.

### Usage
- **QR Menu**: Customer scans → orders → pays.
- **Kiosk**: Customer uses mounted tablet.
> ✅ A POS session must be open to process orders.

Orders appear in:
- **Preparation Display** (if enabled)
- **POS Orders** list

---

## Product Combos

### Use Cases
- **Restaurants**: Choose sides/drinks with main dish.
- **Retail**: Build product sets with options.

### Configuration

#### Step 1: Create Combo Choices
1. Go to **POS > Products > Product Combos > New**.
2. Name combo.
3. Add products → set **Extra Price** (optional).

#### Step 2: Create Combo Product
1. Go to **POS > Products > Products > New**.
2. Set **Product Type = Combo**.
3. Fill **General Info**.
> Combo has **fixed base price**; only extra prices affect total.
4. In **Combo Choices** tab, attach created combos.

### Practical Use
- In POS session, select combo → choose options → **Add to order**.
- Extra prices shown under selections.

---

## Shop Features

### Sales Orders
- Create/pay sales orders directly in POS.

#### Select a Sales Order
1. In POS, click **Quotations/Orders**.
2. Filter by customer/reference.
> Set customer first to narrow list.

#### Apply Down Payment or Settle
- **Down Payment**: Enter % → confirm.
- **Settle**: Pay full balance.
> Down payment auto-deducted when settling.

### Barcodes

#### Configuration
1. In **Inventory > Configuration > Settings**, enable **Barcode Scanner**.

#### Assign Barcodes
- **Products**: In product form, fill **Barcode** field.
- **Employees**: In employee form, set **Badge ID** and **PIN**.

#### Use
- **Scan products**: Adds to cart. Scan multiple times for qty.
- **Log employees**: Scan badge to log in.
- Restrict POS access to barcode login only.

### Serial Numbers and Lots

#### Enable Traceability
- In product **Inventory** tab, select:
  - **Tracking By Unique Serial Number**
  - **Tracking By Lots**

#### Import from Sales Order
- If order has tracked items, POS prompts to **load Lots/Serials**.
- Numbers appear below product; editable via list-view button.

#### Create During Sale
- When adding tracked product, popup appears.
- Enter/scan number → **Enter** to add more.
> ⚠️ Changing qty turns list-view icon **red** → click to fill missing numbers.  
> Not mandatory to complete sale.

### Ship Later
Sell now, ship later (e.g., out of stock, large item).

#### Configuration
1. In **POS > Settings > Inventory**, enable **Allow Ship Later**.
2. Set:
   - **Warehouse**
   - **Route** (optional)
   - **Shipping Policy**:  
     - As soon as possible (partial)  
     - When all ready (full)

#### Use
1. In payment screen, select **customer**.
2. Click **Ship Later** → set date → **Confirm**.
> Delivery order auto-created.  
> Customer must have address.

### Customer Display

#### Configuration
- In **POS > Settings > Connected Devices**, enable **Customer Display**.

#### Local Display
- Connect 2nd screen (HDMI/USB-C).
- In POS session, click **☰ > customer screen icon** → drag to 2nd screen.
- On Odoo Android (dual-screen): use customer screen icon.

#### Remote Display
- From another device, open POS → **⋮ > Customer Display**.
> No same-network requirement.

#### IoT Display
- Connect monitor to **IoT Box**.
- In POS Settings, enable **IoT Box** and select monitor.
> IoT Box and POS must be on same local network.

---

## Restaurant Features

### Floors and Tables
- Manage floor plans & table status (occupied, booked).

#### From Backend
- **POS > Configuration > Floor Plans** → create/edit floors/tables.

#### From Frontend
- In POS session: **☰ > Edit Plan** → add/edit → save (floppy icon).

#### Table Transfer
- **Actions > Transfer/Merge** to move/combine orders.

### Orders Printing
1. In **POS Settings**, enable **Kitchen Printers**.
2. Add/configure printers (IoT or Epson IP).
3. Assign product categories to print.
4. In session, click **Order** to send.
> Ready-to-print items shown in **green**.

### Bills
- Enable **Early Receipt Printing** and **Allow Bill Splitting**.
- **Bill > Print**: provisional bill.
- **Split**: divide items for separate payment.

### Tips
1. In **POS Settings > Payment**, enable **Tips**.
2. Assign a **Tip Product**.
3. Add tips via:
   - On-screen input
   - Tip product selection
   - Adyen terminal
> Enable **Tips after payment** for North American workflows.

---

## Pricing Features

### Discounts
- **Manual Product Discount**: Use **Disc** button.
- **Global Order Discount**:
  - Enable in **POS Settings** → **Discount** button appears.
  - Apply % to entire order.
- **Time-Limited (Pricelists)**:
  - Enable **Pricelists**.
  - Create under **POS > Products > Pricelists**.
  - Set date/product/customer rules.
  - In POS, use **Pricelist** button to apply.

### Discount Tags (Barcode Scanner)
Apply discounts via barcode (e.g., near-expiry items).

#### Requirements
- Barcode scanner.

#### Barcode Format
- Discount tag = prefix + product barcode  
  (e.g., `2250` + lemon barcode = 50% off)

#### Use
1. Scan product.
2. Scan discount tag.
→ Discount auto-applied.

### Loyalty Programs

#### Activate
- In **POS > Configuration > Point of Sale**, enable **Loyalty Program**.
- Click **Create and edit…**.

#### Configure
- **Program Name**: e.g., "Gold Points"
- **Points per Currency**: e.g., 1 per ₹100
- **Points per Product** (optional)
- **Rounding**, **Min Amount** (optional)

#### Add Rewards
- **Reward Type**: Discount or Gift
- **Min Points**, **Value/Product**

#### Use in POS
- Add customer → points earned/available shown.
- Click **Rewards** to redeem.
- Points auto-added to customer record.

#### View History
- In **Sales > Customers > [Profile]** → loyalty tab.

### Pricelists

#### Enable
1. In **POS Settings > Pricing**, enable **Flexible Pricelists**.
2. Choose:
   - **Multiple prices per product**
   - **Advanced price rules (discounts, formulas)**

> Affects Sales & eCommerce too.

#### Create
- **POS > Products > Pricelists > New**

##### Multiple Prices
- Add line: Product, Min Qty, Dates, Fixed Price.

##### Advanced Rules
- **Computation**: Fixed, Discount, Formula
- **Formula options**: Based on cost/price, discount %, extra fee, rounding (e.g., .99), margin
- **Scope**: All, Category, Product
- **Conditions**: Min Qty, Validity

#### Assign to POS
- In **POS Configuration > Pricing**, add pricelists.
- Set **Default Pricelist**.

#### Use in Session
- Click **Pricelist** button → select.
- Prices auto-update.
> Fallback to standard price if conditions unmet.

#### Customer-Specific
- In **Sales > Customers > [Profile] > Sales & Purchase**, set **Pricelist**.
> Auto-applied when customer selected in POS.

### Flexible Taxes (Fiscal Positions)

#### Enable
1. In **POS Settings > Accounting**, enable **Flexible Taxes**.
2. Set **Default Fiscal Position**.
3. Add **Allowed Fiscal Positions**.

#### Create Fiscal Positions
- **Accounting > Configuration > Fiscal Positions > Create**
- **Tax Mapping**: Default Tax → Replacement Tax
- **Account Mapping** (optional)

#### Use in POS
1. Add customer.
2. Click **Tax** button → select fiscal position.
→ Taxes auto-update.

#### Assign to Customer
- In customer **Sales & Purchase** tab, set **Fiscal Position**.
> Auto-applied in POS.

### Cash Rounding

#### Enable Globally
- In **POS Settings > Accounting**, enable **Cash Rounding**.

#### Configure Per POS
1. In **POS Configuration > Accounting**, enable **Cash Rounding**.
2. In **Rounding Method**, click **Create and Edit…**:
   - **Name**: e.g., "Round to 0.05"
   - **Precision**: 0.05
   - **Strategy**: Only "Add rounding line" supported
   - **Profit/Loss Accounts**

#### Use
- When paying with **cash**, total auto-rounded.
- **"Rounding" line item** added to receipt.

### Electronic Shelf Labels (Pricer Integration)

#### Prepare Pricer Account
1. Contact Pricer → create stores, link transceivers.
2. Create **variables** (must match Odoo):
   - `itemId`, `itemName`, `price`, `presentation`, `currency`, `barcode`
3. Create **Template** named `NORMAL`.
4. Enable **API access**.

#### Install Odoo Module
- Apps → search **POS Pricer** → Install.

#### Configure in Odoo
1. **POS > Configuration > Pricer Stores > New**
   - Store Name, Pricer Tenant, Login, Password, Store ID

#### Link Tags to Products
1. In product **Sales** tab → **Pricer** section:
   - Select **Pricer Store**
   - Add **Pricer Tag ID** (1 letter + 16 digits)

#### Sync
- Auto-sync every 12h on change.
- Manual sync (Dev Mode): **Pricer Store** → **Update Tags** or **Update All Tags**

#### Discount Labels
- In **Product Variants**, set **Pricer Sales Pricelist**.
→ **On Sale Price** shown on ESL.

---

## Payment Methods

### QR Code Payments

#### Enable
1. **Accounting > Settings > Fiscal Localization**:
   - Activate country package (e.g., Brazil, Switzerland)
2. In **Customer Payments**, enable **QR codes**.

#### Supported QR Types
| QR Type       | Country        | Module         |
|---------------|----------------|----------------|
| Pix           | Brazil         | `l10n_br`      |
| FPS           | Hong Kong      | `l10n_hk`      |
| QRIS          | Indonesia      | `l10n_id`      |
| PayNow        | Singapore      | `l10n_sg`      |
| QR-bill       | Switzerland    | `l10n_ch`      |
| PromptPay     | Thailand       | `l10n_th`      |
| VietQR        | Vietnam        | `l10n_vn`      |
| EPC/SEPA QR   | Eurozone       | `account_qr_code_sepa` |

> Install module if missing.

#### Create Payment Method
1. **POS > Configuration > Payment Methods > New**
   - Name: "QR Bank Payment"
   - Journal: Bank-type with valid account
   - Integration: **Bank App (QR Code)**
   - QR Format: SEPA or EMV (e.g., PromptPay)

#### Assign to POS
- Add in **POS Configuration > Payments**.

#### Use in POS
1. At payment, select QR method.
2. QR appears → customer scans with banking app.
3. Cashier clicks **Confirm Payment** after transfer.
> ❗ Odoo does **not verify** payment — manual confirmation required.

### Payment Terminals (Razorpay)

#### Get Credentials
From Razorpay Dashboard:
- API Key
- Username
- Device Serial Number

#### Install Module
- Apps → **POS Razorpay** → Install.

#### Create Payment Method
1. **POS > Payment Methods > New**
   - Name: "Razorpay Terminal"
   - Journal Type: Bank
   - Terminal: **Razorpay**
   - Enter credentials
   - Select payment modes (card, UPI, etc.)
   - (Optional) Enable Test Mode

#### Link to POS
- Add in **POS Configuration > Payments**.

#### Use at Checkout
1. Select **Razorpay Terminal**.
2. Terminal shows amount.
3. Customer pays via card/UPI/QR.
4. On success, POS auto-confirms → click **Validate**.

> Ensure terminal battery ≥10%.

---

## Marketing Features

### Storing Contact Details
- **Email**: Saved when sending receipt by email.
- **Phone**: Saved when using WhatsApp/SMS.

> Enable in **POS Settings > Bills & Receipts**: **WhatsApp Enabled** / **SMS Enabled**.

### Email Marketing
1. **POS > Orders > Orders** → select orders.
2. **Actions > Send Email**.
3. Fill/send → optionally save as template.
> - Enter **Mass Mailing Name** for tracking.  
> - New customer auto-created if email not linked.

### WhatsApp Marketing

#### Configuration
1. In **WhatsApp app**, create template:
   - **Applies to**: POS Orders
   - **Category**: Marketing
   - **Phone Field**: Mobile or Customer > Phone
2. **Submit for Approval** → **Allow Multi** (creates server action).

> Edit = re-approve.

#### Send Messages
1. **POS > Orders** → select orders.
2. **Actions > WhatsApp Message**.
3. Choose approved template → **Send Message**.

> Error if no valid template.

---

## UrbanPiper Integration for Online Food Delivery

### Prerequisites
- UrbanPiper subscription
- Odoo Enterprise v18+
- Reseller accounts (Zomato, Swiggy, etc.)

### Get API Credentials
- POS Settings → Food Delivery Connector → **Fill this form**
- UrbanPiper Atlas → Settings → API Access → copy **Username** & **API Key**

### Enable in POS
1. In **Food Delivery Connector**:
   - Enable **Urban Piper**
   - Enter credentials
   - Select platforms (Zomato, Swiggy, etc.)
   - **+ Create Store**

### Make Products Available
- In **POS > Products**:
  - Open product → **POS tab**
  - Fill **Available on Food Delivery**
  - Set **Meal Type**, **Is Recommended**, **Is Alcoholic** (optional)
- Bulk update via list view.

### Synchronize
- In **Food Delivery Connector**, click **Sync Menu** (~2–3 min).

### Go Live
1. UrbanPiper Atlas → Locations → **Request to go Live**
2. Choose platforms → enter **Platform ID/URL** → **Request**

### Manage Orders
- Orders arrive via popup or icon.
- Stages:
  - **New** → **Accept** → **Acknowledged**
  - **Ongoing** → **Mark as Ready** → **Paid**
- **Reject**: choose reason.
> Swiggy/Deliveroo/JustEat/HungerStation: no direct rejection.

---

## Reporting

1. Go to **POS > Reporting > Orders**  
   or from POS dashboard: **⋮ > Reporting > Orders**.
2. View in **Graph** or **Pivot**.
3. Apply **filters** and **grouping**.