# Restaurant – Odoo POS Guide

## 🔧 To Set Up Odoo
- 📄 Reference: [Odoo Setup Guide](https://docs.google.com/document/d/1B2PD9XkewpMPsY9tOA1C7F6PuS5HcG2dqokLzn9SafU/edit?tab=t.0)
- 🔐 **Default Credentials**:  
  - **Email:** `admin`  
  - **Password:** `admin`

---

## 🏪 Opening the Restaurant

1. Go to the main **Menu** (☰).
2. Click **Point of Sale**.
3. Under the **Restaurant** section, click **Continue Selling**.

> This opens the floor plan view for your restaurant.

---

## 🍽️ Taking an Order for a Table

1. **Click a table** on the floor plan to enter the ordering screen.
2. In the **middle-left panel**, click **Book Table** (if not already booked).
3. Click the **Customer** button (bottom-left) to:
   - Select an existing customer, or  
   - Create a new one.
4. Browse the product list and **select a food item**.
   - Available **varieties** (e.g., spice level, size) will appear.
5. Choose a variety and click **Add**.
6. The item appears on the **left cart panel** with:
   - Quantity
   - Price
7. Use the **keyboard** to adjust quantity or price manually (if allowed).
8. The **table icon** updates to show the total number of items ordered.
9. Once ready, click **Order** → it changes to **Payment**.
10. Click **Payment** to:
    - View the total amount
    - Select a payment method (**Cash**, **Card**, etc.)
11. To change the payment method, click the ❌ (clear) icon next to it.
12. (Optional) Tick **Invoice** to generate a formal invoice.
13. Click **Validate** to complete the transaction.
14. You’ll see a **Payment Successful** screen showing:
    - Order summary
    - GST/tax details

---

## 📦 Creating a New Product

1. Open the **Menu** (top-right corner in POS session).
2. Click **Create Product**.
3. Fill in the product details in the pop-up form:
   - Name
   - Price
   - Category (e.g., Food, Drink)
   - Available Variants (optional)
4. Click **Save** to add it to your catalog immediately.

> The new product will appear in all relevant categories during ordering.

---

## 🗺️ Editing the Floor Plan

1. Open the **right-side Menu** (three-dot or hamburger icon).
2. Click **Edit Plan**.
3. Use the toolbar to:
   - **Add tables** (drag from palette)
   - **Move/resize** existing tables
   - **Delete** or **rotate** items
4. Click **Save** (floppy disk icon) when finished.

> Changes are saved per POS configuration and visible across all sessions.

---

## 🧭 Switching Floor View

1. Open the **right-side Menu**.
2. Click **Switch Floor View**.
   - Toggles between:
     - **Default layout** (standard view)
     - **Custom layout** (your edited floor plan)

> Useful for comparing or reverting changes.

---

## ⚠️ Notes & Tips

- ✅ **Green tables** = currently **booked/occupied**.  
- 🔓 **To release a table**:
  - Click the table
  - In the left panel, select **Release Table**
- 🍱 Use **Food** and **Drinks** filters on the order screen to quickly find items.
- 🖨️ Ensure **kitchen printers** are configured to auto-print orders (via POS settings).
- 📱 Customers can also order via **QR self-ordering** if enabled.

---

## 🧾 Complete Order Flow (Visual)

![Order Flow](https://github.com/user-attachmentsibles/b8936b44-a1c8-4926-8097-b67a5cb27710)

> *Illustrates the end-to-end process from table selection to payment validation.*