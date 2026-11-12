# Employee Onboarding Documentation

---

## 1. Overview

The **Employee Onboarding** feature in **Odoo 19 Community** was tested to understand the default onboarding workflow and verify how onboarding plans are assigned to employees based on their department.

The testing focused on validating whether Odoo automatically applies the correct onboarding plan without requiring any Python or XML customization.

---

## 2. Objectives

The Employee Onboarding testing was performed to:

- Understand the default Employee Onboarding workflow.
- Explore the standard onboarding plans available in Odoo.
- Create department-specific onboarding plans.
- Verify department-based onboarding assignment.
- Confirm that onboarding plans are automatically applied based on the employee's department.
- Validate the functionality without custom development.

---

## 3. Environment

| Item | Details |
|------|---------|
| Odoo Version | Odoo 19 Community |
| Module | Employees |
| Feature | Employee Onboarding |

---

## 4. Testing Process

### 4.1 Explored the Default Onboarding Plan

Navigated to:

```text
Employees → Configuration → Onboarding / Offboarding → Employee Plans
```

Reviewed the default onboarding plans:

- Onboarding
- Offboarding

Verified the default onboarding activities:

- Setup IT Materials
- Plan Training
- Training

---

### 4.2 Created Departments

Created the following departments:

- IT
- Development
- HR

Navigation:

```text
Employees → Departments → New
```

---

### 4.3 Created Department-Specific Onboarding Plans

Created separate onboarding plans for each department.

#### IT Onboarding

Department:

- IT

Activities:

- Setup IT Materials
- Assign Laptop
- Create Email

---

#### Developer Onboarding

Department:

- Development

Activities:

- GitHub Access
- IDE Setup
- Project Access

---

#### HR Onboarding

Department:

- HR

Activities:

- Document Verification
- Employee Orientation
- HR Policy Training

Navigation:

```text
Employees → Configuration → Onboarding / Offboarding → Employee Plans → New
```

---

### 4.4 Created Employees

Created employees for different departments.

| Employee | Department |
|----------|------------|
| Bhuvana | IT |
| Anusha | Development |
| Jyothika | HR |

Assigned the **Administrator** as the manager for all employees.

Navigation:

```text
Employees → Employees → New
```

---

### 4.5 Tested Employee Onboarding

Opened each employee record and launched the onboarding plan.

Action:

```text
Employee → Launch Plan
```

Initially, the default onboarding plan was assigned to all employees.

---

### 4.6 Verified Department-Based Onboarding

Assigned the appropriate department to each onboarding plan.

Examples:

| Onboarding Plan | Department |
|-----------------|------------|
| IT Onboarding | IT |
| Developer Onboarding | Development |
| HR Onboarding | HR |

After configuring the department, tested the onboarding process again.

---

### 4.7 Final Testing Results

#### IT Employee

Employee:

- Bhuvana

Department:

- IT

Result:

Only the **IT Onboarding** activities were displayed.

Activities:

- Setup IT Materials
- Assign Laptop
- Create Email

---

#### Development Employee

Employee:

- Anusha

Department:

- Development

Result:

Only the **Developer Onboarding** activities were displayed.

Activities:

- GitHub Access
- IDE Setup
- Project Access

---

#### HR Employee

Employee:

- Jyothika

Department:

- HR

Result:

Only the **HR Onboarding** activities were displayed.

Activities:

- Document Verification
- Employee Orientation
- HR Policy Training

---

## 5. Observation

During testing, the default onboarding plan was initially assigned to every employee because it was available for all departments.

After configuring each onboarding plan with its respective department, Odoo automatically assigned the onboarding plan that matched the employee's department.

This behavior worked using the standard Odoo functionality without any customization.

---

## 6. Benefits

The Employee Onboarding feature provides:

- Department-based onboarding management.
- Automatic onboarding plan assignment.
- Organized onboarding activities.
- Improved employee onboarding workflow.
- Reduced manual effort.
- Standard functionality without custom development.

---

## 7. Current Status

Successfully verified:

- Default Employee Onboarding feature.
- Department creation.
- Department-specific onboarding plans.
- Employee creation.
- Manager assignment.
- Onboarding plan launch.
- Automatic department-based onboarding assignment.

---

## 8. Conclusion

Successfully tested the standard **Employee Onboarding** feature in **Odoo 19 Community**.

The testing confirmed that onboarding plans can be configured for specific departments, and Odoo automatically applies the appropriate onboarding plan based on the employee's assigned department.

This functionality works using the built-in Employee Onboarding feature without requiring any Python or XML customization.
