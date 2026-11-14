## Compensatory Leave Configuration in Odoo

## Overview

This document explains how compensatory leave works in Odoo 19 (Time Off). An employee who worked on a public holiday or Sunday records that day as the `Worked Date` when applying, and admins can see it in a dedicated report.


## 1. Configure the Leave Type

### Step 1: Open the leave type

Go to `Time Off` → `Configuration` → `Time Off Types` and open `Compensatory leave`.

### Step 2: Enable the flag

Tick `Is Compensatory Leave` and save. This is a one-time setup.


## 2. Apply for Compensatory Leave

### Step 1: Create the request

Go to `Time Off` → `New`, select `Compensatory leave` and choose the leave date.

### Step 2: Enter the worked date

Enter the holiday or Sunday worked in `Worked Date` (required), then click `Submit Request`.


## 3. Approve the Request

Go to `Time Off` → `Management` → `Time Off`, open the request and approve it.


## 4. View the Report

Go to `Time Off` → `Reporting` → `Compensatory Leave Report`. It shows the employee, compensatory date, worked date and status.


## 5. Dashboard

On the Employee Analytics Dashboard, `Leaves Taken` does not count compensatory leave. It is still listed in the employee's `Leave` tab, tagged `Not counted`.


## Notes

- Only employees who applied for compensatory leave appear in the report.
- The `Worked Date` is not checked against holidays or Sundays. The approver confirms it.
