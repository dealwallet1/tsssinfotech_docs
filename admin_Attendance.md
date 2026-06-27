# Attendance Module (Admin Setup – Barcode, GPS & Alerts)


## Overview

This guide explains how to configure attendance in Odoo including:
- Barcode setup
- Kiosk Mode
- GPS tracking
- Late and absent email alerts

---

## 1. Install Attendance Module

- Go to **Apps**
- Search for **Attendances**
- Click **Install**

---

## 2. Configure Employee Barcode

- Go to **Employees → Employees**
- Select an employee
- Enter a unique value in **Barcode** (Example: EMP001)
- Click **Save**

---

## 3. Enable Kiosk Mode

- Go to **Attendances**
- Click **Kiosk Mode**
- Select **Barcode Scanning**

---

## 4. Setup Kiosk Device

- Use a desktop or tablet
- Keep Kiosk screen open
- Connect barcode scanner (if available)

---

## 5. Enable GPS Location Tracking

- Ensure browser location permission is allowed
- Capture latitude and longitude during check-in/check-out
- Store location in attendance records

---

## 6. Configure Late Check-In Rule

Define email notification time (Example: 10:00 AM)
- Create automated action:
- Collect attendance records for the day
- Identify employees who have not checked in before 10:00 AM
- Generate late attendance report
- Send notification email to the configured recipients
- Execute automatically every day at 10:00 AM

---

## 7. Configure Email Alerts (Late)

- Create email template
- Send notification to:
  - Admin
  - Team Leads

- Include employee list

---

## 8. Configure Absent Alert

- At end of day:
  - Identify employees with no attendance

- Send email:
  - List of absent employees
  - To Admin / HR

---

## 9. Verify Records

- Go to **Attendances → Records**
- Check:
  - Check-in / Check-out
  - Employee details
  - Location data

---

## Conclusion

Admins can manage attendance, track locations, and automate alerts for better monitoring and control.
