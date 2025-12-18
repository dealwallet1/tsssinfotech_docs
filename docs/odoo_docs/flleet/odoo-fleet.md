# Odoo Fleet Management Documentation

## Table of Contents
1. Introduction  
2. Vehicle Manufacturers  
   - View Manufacturers  
   - Add a Manufacturer  
3. Vehicle Models  
   - Add a Model  
   - Model Configuration  
4. Model Categories  
   - Add a New Category  
5. Adding Vehicles  
   - Vehicle Form Fields  
   - Driver Management  
6. Services & Maintenance  
   - Create Service Records  
   - Service Stages  
7. Accident Management  
   - Logging Accidents  
   - Accident Reporting  
8. Settings  
   - Contract Alerts  
   - Vehicle Request Limits  

---

## 1. Introduction

Odoo’s **Fleet** application helps businesses manage company vehicles efficiently.  
It allows tracking of vehicle manufacturers, models, drivers, maintenance services, accidents, and contracts.

This documentation provides a **step-by-step guide** to configuring and managing fleet operations using the Odoo Fleet module.

---

## 2. Vehicle Manufacturers

### View Manufacturers

1. Go to **Fleet app → Configuration → Manufacturers**.
2. By default, the **With Models** filter is applied.
3. Remove the filter to view all manufacturers.
4. Manufacturers are displayed alphabetically with logos and model counts.

### Add a Manufacturer

1. Click **New** (top-left).
2. Enter the **Name** of the manufacturer.
3. Upload a **Logo** (optional).
4. Click **Save**.

---

## 3. Vehicle Models

### Add a Model

1. Navigate to **Fleet app → Configuration → Models**.
2. Click **New**.
3. Enter the following details:
   - **Model Name**: e.g., *X2*
   - **Manufacturer**: Select or create a new one
   - **Vehicle Type**: Car or Bike
   - **Category**: Optional classification
4. Click **Save**.

### Model Configuration

#### Information Tab
- **Seats Number**: Passenger capacity
- **Doors Number**: Number of doors
- **Model Year**: Manufacturing year
- **Trailer Hitch**: Enable if applicable
- **Fuel Type**: Diesel, Petrol, Electric, etc.
- **CO₂ Emissions**: g/km
- **Transmission**: Manual or Automatic
- **Horsepower / Power**: Engine specifications

#### Vendors Tab
- Add vendors where the vehicle can be purchased
- Click **Add** to select existing vendors or **New** to create one

---

## 4. Model Categories

### Add a New Category

1. Go to **Fleet app → Configuration → Categories**.
2. Click **New**.
3. Enter the category name (e.g., *SUV*).
4. Click **Save**.
5. (Optional) Drag and reorder categories as needed.

---

## 5. Adding Vehicles

### Vehicle Form Fields

1. Navigate to **Fleet app → Fleet → Vehicles**.
2. Click **New**.
3. Fill in the required details:
   - **Model** (mandatory)
   - **License Plate**
   - **Tags** (optional)
4. Click **Save**.

---

## Driver Management

### Assign a Driver

1. In the **Driver** section:
   - Select an existing driver, or
   - Click **Create and Edit** to add a new driver
2. Enter driver details (name, contact information).
3. Set **Future Driver** if a reassignment is planned.
4. Define the **Assignment Date**.

### Vehicle Details

- **Order Date**: Vehicle purchase date
- **Registration Date**: Official registration date
- **Chassis Number (VIN)**: Unique vehicle identifier
- **Last Odometer**: Current mileage
- **Location**: Vehicle storage location

---

## 6. Services & Maintenance

### Create Service Records

1. Go to **Fleet app → Fleet → Services**.
2. Click **New**.
3. Enter:
   - **Service Type** (e.g., Oil Change)
   - **Vehicle**
   - **Vendor**
   - **Odometer Value**
   - **Cost**
4. Click **Save**.

### Service Stages

- **New**: Requested
- **Running**: In progress
- **Completed**: Finished
- **Cancelled**: Not performed

Stages can be updated via:
- Individual service form
- Kanban view (drag and drop)

---

## 7. Accident Management

### Logging Accidents

1. Go to **Fleet app → Fleet → Services**.
2. Click **New**.
3. Set:
   - **Service Type**:  
     - *Accident – Driver’s Fault*  
     - *Accident – No Fault*
   - **Description**: Damage details
   - **Notes**: Accident circumstances
4. Attach documents (police report, estimates).
5. Click **Save**.

### Accident Reporting

- View total accident costs in the **Services Dashboard**
- For detailed analysis, go to **Reporting → Costs**
- Filter by **Vehicle** to review repair expenses

---

## 8. Settings

### Contract Alerts

1. Navigate to **Fleet app → Configuration → Settings**.
2. Set **End Date Contract Alert** (e.g., 30 days before expiry).
3. Assigned users receive email notifications.

### Vehicle Request Limits (Belgium Only)

1. Configure **New Vehicle Request Limit**.
2. Employees can request vehicles only if available count is within the limit.

---
