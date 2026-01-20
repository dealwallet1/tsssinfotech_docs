# Razorpay Payment Gateway Integration with Odoo

## 1. Overview

Razorpay is a leading online payment service provider based in India. It supports **100+ payment methods**, including:

- Credit/Debit Cards  
- UPI  
- Net Banking  
- Wallets  
- Recurring Payments  

Odoo provides **native integration with Razorpay** for Indian companies, enabling seamless online payment processing for:

- Invoices  
- eCommerce Orders  
- Subscriptions  

---

## 2. Eligibility & Important Notes

Before proceeding, note the following constraints:

- ✅ **Available only for Indian companies**  
- ❌ **Test mode is not supported** in the automatic account creation flow  
- ✅ **Manual configuration supports Test Mode**  
- 🔁 **Recurring payments** require explicit activation by Razorpay Support  

---

## 3. Method 1: Create & Connect Razorpay Account Directly from Odoo  
*(Indian Companies Only)*

### Description

This method allows you to **create or link a Razorpay account directly from Odoo** without manually handling API keys.

> ⚠️ **This flow does not support Test Mode.**

### Step-by-Step Process

#### Step 1: Open Razorpay Payment Provider in Odoo
- Log in to Odoo as an **Administrator**
- Navigate to:  
  **Accounting → Configuration → Payment Providers**
- Open **Razorpay**
- Click **Connect**

#### Step 2: Account Creation / Linking
- **If you don’t have a Razorpay account**:  
  - Complete the Razorpay account creation process  
  - Enter verification codes when prompted  

- **If you already have a Razorpay account**:  
  - Enter your Razorpay credentials  
  - Select the account to link (if multiple exist)  
  - Click **Continue**

#### Step 3: Authorization
- Review the permissions requested by Odoo  
- Click **Authorize**

✅ Upon successful authorization:
- You’re redirected back to Odoo  
- The Razorpay provider state is set to **Enabled**  
- **Razorpay is now ready to process live payments in Odoo**

---

## 4. Method 2: Manual Configuration (API Keys & Webhooks)  
*(Recommended for Testing & Advanced Control)*

Use this method when you:
- Want to use **Test Mode**
- Prefer **manual control** over credentials and webhooks
- Need to configure **webhooks** for real-time payment status updates

---

## 5. Razorpay Dashboard Configuration

### Step 1: Log in to Razorpay Dashboard
- Go to [https://dashboard.razorpay.com](https://dashboard.razorpay.com)
- Log in with your Razorpay account

### Step 2: Enable Test Mode (Optional)
- Go to the **Payments** tab
- In the left menu, toggle **Test Mode ON**
- Use this for **testing without charging real money**
- Toggle **OFF** before going live

### Step 3: Generate API Keys
- Navigate to:  
  **Account & Settings → Website and App Settings → API Keys**
- Copy and securely store:
  - **Key ID**
  - **Secret Key**

> These will be entered in Odoo.

### Step 4: Configure Webhooks
- Go to:  
  **Account & Settings → Website and App Settings → Webhooks**
- Click **Add New Webhook**
- Enter the **Webhook URL**:  https://your-odoo-domain.com/payment/razorpay/webhook
- Set a **Webhook Secret** (any secure password — remember it!)
- Enable the following **events**:
- `payment.authorized`
- `payment.captured`
- `payment.failed`
- `refund.failed`
- `refund.processed`
- Click **Create Webhook**

> 📌 **Save the webhook secret** — it’s required in Odoo.

### 🔁 Important: Recurring Payments
- To accept **subscriptions or recurring payments**:
- Razorpay must **explicitly enable** this feature
- **Raise a support request** with Razorpay to activate recurring payments

---

## 6. Odoo Configuration (Manual Method)

### Step 1: Activate Developer Mode
- Go to **Settings**
- Scroll down and click **Activate Developer Mode**

### Step 2: Configure Razorpay in Odoo
- Navigate to:  
**Accounting → Configuration → Payment Providers**
- Open **Razorpay**
- Go to the **Credentials** tab
- Enter:
- **Key ID**
- **Key Secret**
- **Webhook Secret**  
*(Use values saved from Razorpay Dashboard)*

### Step 3: Final Settings
- Set **Payment Flow** (e.g., automatic capture)
- Ensure compatibility with **Invoices/eCommerce** as needed
- Set **State**:
- **Test** → for sandbox testing
- **Enabled** → for live transactions
- Click **Save**

✅ **Razorpay is now fully configured in Odoo.**

---

## 7. Important Operational Notes

### Manual Capture Limitations
- If Odoo is configured for **manual capture**:
- ❌ Razorpay **does not support manual voiding**
- ⏳ Transactions **not captured within 5 days** are **automatically voided** by Razorpay

> 👉 **Recommendation**:  
> Use **automatic capture** unless your business process **strictly requires** manual authorization.

---

# Custom POS Razorpay Integration

---

## Step 8: Module Registration and Initialization

At this stage, the Razorpay POS integration module is registered within Odoo.

- Odoo recognizes the module as a POS extension.
- Dependencies such as Point of Sale and Razorpay payment services are declared.
- Required assets for POS (JavaScript, backend routes, and permissions) are loaded automatically.
- Security rules ensure only authorized users can interact with Razorpay features.

**Result:**  
The module becomes available in Odoo and is ready to enhance POS payment functionality.

---

## Step 9: POS Interface Loads Razorpay Capabilities

When a cashier opens the Point of Sale:

- The standard POS interface loads.
- Razorpay-related payment capabilities are injected into the POS environment.
- Razorpay checkout services are prepared in the background.

**Result:**  
The POS is Razorpay-enabled without altering the standard user interface.

---

## Step 10: Cashier Selects Razorpay Payment Method

During checkout:

- The cashier selects a Razorpay-based payment method (UPI, Card, Wallet, or Payment Link).
- The POS identifies this as a digital payment that requires external confirmation.

**Result:**  
The POS switches from a standard payment flow to a Razorpay-controlled flow.

---

## Step 11: POS Intercepts Order Validation

Before completing the order:

- Odoo temporarily blocks the default order validation.
- Payment confirmation becomes mandatory before order finalization.
- This prevents unpaid or partially paid orders from being validated.

**Result:**  
Orders cannot be completed without verified payment.

---

## Step 12: Payment Experience Selection

The system determines how the customer will pay:

- **Popup Checkout** – Payment completed directly on the POS screen.
- **Payment Link** – A secure link is generated and shared with the customer’s device.

**Result:**  
Flexible payment options are offered without manual workarounds.

---

## Step 13: Secure Backend Communication with Razorpay

Once the payment flow is chosen:

- The POS sends a secure request to the Odoo backend.
- The backend communicates with Razorpay using configured credentials.
- Sensitive payment data remains protected on the server side.

**Result:**  
Payment requests are created securely and compliantly.

---

## Step 14: Razorpay Processes the Payment

Depending on the selected payment method:

- **Popup Flow:**  
  - Razorpay opens a secure checkout window.
  - Customer completes the transaction.
  - Razorpay returns the payment status.

- **Payment Link Flow:**  
  - A secure payment URL is generated.
  - Customer completes payment on their device.
  - Odoo monitors and retrieves the payment status.

**Result:**  
Payments are processed externally but tracked internally.

---

## Step 15: Payment Status Verification

After the payment attempt:

- Odoo verifies the transaction status with Razorpay.
- Only successful and confirmed payments are accepted.
- Failed or pending payments prevent order completion.

**Result:**  
Financial accuracy and integrity are enforced.

---

## Step 16: POS Marks Payment as Completed

When the payment is confirmed:

- The POS updates the payment line as completed.
- The paid amount is reconciled with the order total.
- No manual confirmation is required from the cashier.

**Result:**  
POS reflects real-time, accurate payment status.

---

## Step 17: Order Validation and Completion

With payment verified:

- The POS allows the order to be validated.
- Receipt generation (print or digital) becomes available.
- Order data is saved in Odoo for reporting and accounting.

**Result:**  
A fully paid and validated POS order is created.

---

## Step 18: Security and Access Control Enforcement

Throughout the entire flow:

- Access rights restrict Razorpay usage to authorized POS users.
- Backend endpoints are protected against unauthorized access.
- Payment data is securely logged for auditing purposes.

**Result:**  
The system remains secure and compliant with financial standards.

---

## Step 19: Business Benefits

This integration delivers:

- Guaranteed payment validation before order completion
- Faster checkout using UPI and digital payments
- Secure handling of financial credentials
- Seamless customer experience
- Accurate sales and accounting records

---

## Final Summary

The **Custom POS Razorpay Integration** enhances Odoo POS by:

- Adding modern, India-compliant digital payment methods
- Enforcing strict payment verification
- Maintaining security and audit compliance
- Providing a smooth checkout experience for customers and staff

This flow is fully aligned with **Odoo POS standards** and **Razorpay payment compliance**, making it suitable for real-world production environments.

---
