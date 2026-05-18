# Pharmacy Inventory Management System in Odoo

---

## 1. Overview

This module is developed to manage pharmacy inventory efficiently using Odoo. It handles medicine tracking, batch management, expiry control, stock updates, and alerts.

The system ensures that expired medicines are not sold and stock is always up to date.

---

## 2. Key Features Implemented

### 2.1 Product (Medicine) Management

- Created medicines as **Storable Products**
- Added:
  - Product Name  
  - Category  
  - Cost Price  
  - Sale Price  
  - GST/Tax  
  - Supplier Details  
- Enabled **Lot/Batch Tracking**

---

### 2.2 Batch & Expiry Management

- Enabled:
  - Lots/Serial Numbers  
  - Expiration Dates  

- Created batches with:
  - Batch Number  
  - Expiration Date  
  - Alert Date  

**Example:**

- Batch1 → Exp: Jan 2025 → Qty: 15  
- Batch2 → Exp: Mar 2026 → Qty: 20  

---

### 2.3 FEFO (First Expired First Out)

- Configured **Removal Strategy = FEFO**
- System automatically sells medicines with earliest expiry first  

---

### 2.4 Stock Management

- Added stock using **Physical Inventory**
- Features:
  - View current stock  
  - Update stock manually  
  - Track stock per batch  

---

### 2.5 Low Stock Alert

- Configured **Minimum Quantity**
- Alerts shown when stock goes below minimum level  

---

### 2.6 Expiry Alerts

- Configured **Alert Date**
- System warns before medicine expiry  

---

### 2.7 Lot-wise Stock Tracking

- Each batch has:
  - Separate quantity  
  - Separate expiry date  

- Enables easy tracking of stock per batch  

---

## 3. Workflow

Create Product → Enable Lot Tracking → Create Batch → Add Expiry Date → Add Stock → Apply FEFO → Sell Product (Oldest Expiry First)

---

## 4. Pharmacy-Specific Logic

- Medicines tracked using Batch Number  
- Expiry dates monitored  
- FEFO applied  
- Alerts for expiry and low stock  

---

## 5. Benefits

- Avoids selling expired medicines  
- Accurate stock management  
- Easy batch tracking  
- Automated updates  
- Improved safety  

---

## 6. Future Enhancements

- Block sale of expired medicines  
- Barcode scanning  
- Purchase to auto batch creation  
- Sales integration  
- Expiry reports  


## 8. Conclusion

The Pharmacy Inventory Management System implemented in Odoo provides an efficient and reliable solution for managing medicine stock with batch and expiry tracking.

By using features such as lot tracking, FEFO removal strategy, and automated alerts, the system ensures accurate inventory control and prevents the sale of expired medicines. It simplifies stock management, improves operational efficiency, and enhances safety in pharmacy operations.

Overall, the implementation demonstrates how Odoo can be effectively used to build a structured and scalable pharmacy inventory management system.

