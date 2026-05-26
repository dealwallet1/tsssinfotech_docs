# Pharmacy Inventory Module — Configuration Explanation (Odoo)

---

## 1. Overview

This document explains the configuration steps required to set up the Pharmacy Inventory Module in Odoo. It focuses on enabling key features such as batch tracking, expiry management, FEFO logic, and stock alerts.

---

## 2. Expiry Date Tracking Setup

### Steps:

1. Go to **Inventory → Configuration → Settings**
2. Enable:
   - Lots & Serial Numbers  
   - Expiration Dates  
3. Click **Save**

### Purpose:

- Enables tracking of medicine expiry dates  
- Activates expiry-related fields in the system  

---

## 3. Batch (Lot) Tracking Setup

### Steps:

1. Go to **Inventory → Products → Open Medicine**
2. Go to **Inventory Tab**
3. Set **Tracking = By Lots**
4. Click **Save**

### Purpose:

- Tracks medicines using batch numbers  
- Maintains separate expiry and quantity for each batch  

---

## 4. Expiry Alert Configuration

### Steps:

1. Go to **Inventory → Products → Lots/Serial Numbers**
2. Create a Lot  
3. Enter:
   - Expiration Date  
   - Alert Date  

### Purpose:

- Generates alerts before medicine expiry  
- Helps in proactive stock management  

---

## 5. FEFO (First Expired First Out)

### Steps:

1. Go to **Inventory → Configuration → Product Categories**
2. Open Product Category  
3. Set **Removal Strategy = FEFO**
4. Click **Save**

### Purpose:

- Ensures medicines with earliest expiry are sold first  
- Prevents loss due to expired stock  

---

## 6. Stock Addition (Physical Inventory)

### Steps:

1. Go to **Inventory → Operations → Physical Inventory**
2. Click **New**
3. Add:
   - Product  
   - Location  
   - Lot  
   - Quantity  
4. Click **Apply**

### Purpose:

- Adds stock into the system  
- Updates inventory quantities  

---

## 7. Low Stock Alert Setup

### Steps:

1. Go to **Inventory → Products**
2. Open product  
3. Set **Minimum Quantity** in Inventory Tab  

### Purpose:

- Alerts when stock falls below minimum level  
- Helps in timely replenishment  

---

## 8. Lot-wise Stock Tracking

### Steps:

1. Create multiple lots  
2. Assign quantity and expiry for each lot  

### Purpose:

- Tracks stock batch-wise  
- Identifies expiring medicines easily  

---

## 9. Conclusion

The configuration of the Pharmacy Inventory Module in Odoo ensures efficient stock management by enabling batch tracking, expiry monitoring, FEFO strategy, and automated alerts.

This setup helps maintain accurate inventory, reduces wastage due to expired medicines, and improves overall pharmacy operations.
