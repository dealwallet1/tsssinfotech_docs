# Odoo Construction Module – User Roles & Access Rights

This document serves as a comprehensive guide to configuring **user roles and access rights** in the custom **Odoo Construction module**.  
It is designed to help administrators **quickly and effectively manage permissions without writing any code**, using Odoo’s standard Admin UI and Studio tools.

📚 **Reference:**  
[Odoo 18.0 Access Rights Documentation](https://www.odoo.com/documentation/18.0/applications/general/users/access_rights.html)

---

## 👥 User Role Overview

| Role | Responsibility | Key Permissions Summary |
|-----|---------------|-------------------------|
| Project Manager | Oversees full project lifecycle | Full access to projects, BoQs, tasks; limited HR and vendor access |
| Site Manager | Executes and monitors site-level work | Task updates, attendance, material request visibility |
| Vendor | Supplies materials and external workforce | Access to RFQs, Purchase Orders, and invoices only |
| Customer | End-client monitoring progress and invoices | Read-only access to own project and invoice data |
| Project Engineer | Manages project execution and coordinates teams | Full project and task access; limited HR and Accounting |
| Site Engineer | Tracks progress and logs timesheets on-site | Access to tasks, planning, and documents only |

> Portal links or embedded forms should be used to provide access for **Vendors** and **Customers**.

---

## 🔐 Access Matrix (Summary)

| Role | Create Project | View Tasks | Place Purchase | Approve BoQ | Edit Attendance |
|----|---------------|------------|---------------|------------|----------------|
| Project Manager | ✅ | ✅ | ✅ | ✅ | ❌ |
| Site Manager | ❌ | ✅ | ❌ | ❌ | ✅ |
| Vendor | ❌ | ❌ | ✅ (Assigned) | ❌ | ❌ |
| Customer | ❌ | ✅ (Read-only) | ❌ | ❌ | ❌ |
| Project Engineer | ✅ | ✅ | ✅ | ✅ | ✅ |
| Site Engineer | ❌ | ✅ | ❌ | ❌ | ✅ |

---

## 🛠 How to Configure Roles (No Code Required)

### 1️⃣ Create Custom User Groups
Navigate to:

**Settings → Users & Companies → Groups**

Steps:
1. Click **Create**
2. Enter a group name (example: `Construction / Site Engineer`)
3. Assign users to the group
4. Inherit required groups from core Odoo modules (Project, Timesheets, etc.)

---

### 2️⃣ Assign Groups to Users
Navigate to:

**Settings → Users → Select User → Access Rights**

Steps:
- Add the relevant Construction group(s)  
  Example: `Construction / Project Engineer`

---

### 3️⃣ Restrict Menu Visibility (Developer Mode)
Navigate to:

**Settings → Technical → User Interface → Menu Items**

Steps:
- Locate the menu to restrict
- Set the **Groups** field to the allowed user groups
- Save changes

---

### 4️⃣ Configure Access Control Lists (ACLs)
Navigate to:

**Settings → Technical → Security → Access Control Lists**

Steps:
- Grant Create, Read, Write, and Delete permissions per model
- Ensure ACLs align with the access matrix defined above

---

### 5️⃣ Create Record Rules (Optional – Row-Level Security)
Navigate to:

**Settings → Technical → Security → Record Rules**

Example: Restrict Site Manager access to assigned sites only.

```python
['|', ('user_id', '=', user.id), ('assigned_site_id.user_id', '=', user.id)]

---

## 🎯 Custom Role Configuration

---

## 🏗️ Project Engineer

### Responsibilities
Oversee site execution, manage project teams, and coordinate vendors to ensure timely delivery of construction activities.

### Group Name
`Construction / Project Engineer`

### Inherited Groups

| Application | Group |
|------------|------|
| Project | Project / Administrator |
| Timesheets | Timesheets / User: All Timesheets |
| Documents | Documents / User |
| Field Service | Field Service / User |
| Planning | Planning / User |
| Task Tools | Use Task Dependencies |
| Billing Tools | Use Time Billing |

### Menus Unlocked
- Project Configuration
- All Timesheets
- Planning Reports
- Documents

---

## 🧱 Site Engineer

### Responsibilities
Track daily site progress, update tasks, and log operational details from the construction site.

### Group Name
`Construction / Site Engineer`

### Inherited Groups

| Application | Group |
|------------|------|
| Project | Project / User |
| Timesheets | Timesheets / User: All Timesheets |
| Documents | Documents / User |
| Field Service | Field Service / User |
| Planning | Planning / User |

### Menus Unlocked
- My Planning
- My Timesheets
- Site Tasks

---

## 🧑‍💼 Customer (Portal-Style Access)

### Responsibilities
View assigned project status, milestones, and invoices without accessing internal operations.

### Group Name
`Construction / Customer`

### Characteristics
- No inherited internal groups
- No access to backend menus
- Access limited strictly through portal

### Record Rules

| Model | Domain Rule |
|------|-------------|
| appointment.slot | `[('staff_user_ids', 'in', [user.id])]` |
| appointment.type | `[('create_uid', '=', user.id)]` |

Access should be provided using **portal links or embedded forms** only.

---

## 🛒 Vendor

### Responsibilities
Respond to RFQs, submit invoices, and manage delivery-related documents.

### Group Name
`Construction / Vendor`

### Access Scope
- View assigned RFQs
- View assigned Purchase Orders
- Upload invoices
- No access to internal projects, accounting, or HR data

---

## 🛠 Field-Level Customizations

---

### 🎯 Filter Vendor Field in Purchase Orders

**Objective:**  
Ensure that only vendors (not all contacts) appear in the Vendor field of Purchase Orders.

**Steps (Using Studio):**
1. Navigate to **Purchase → Create/Edit Purchase Order**
2. Open **Studio (🛠️)**
3. Select the **Vendor (`partner_id`)** field
4. Apply the domain below:

```python
[('supplier_rank', '>', 0)]


---

## 🎯 Restrict Task Assignee to Employees

### Objective
Ensure that tasks can be assigned **only to users who are linked to an Employee record**, preventing assignment to inactive or non-operational users.

### Steps
1. Navigate to **Project → Task Form**
2. Open **Studio**
3. Select the **Assignee** field (`user_id` or `partner_id`)
4. Apply the following domain:

```python
[('employee_id', '!=', False)]


---

## 🧑‍💼 Add Employee Column in User List View

### Objective
Provide administrators with a clear and consolidated view of which **User accounts are linked to Employee records**, enabling easier auditing and user management.

### Steps
1. Navigate to **Settings → Users**
2. Switch to **List View**
3. Open **Studio**
4. Add the field **`employee_id`**
5. Save and close Studio

### Result
Administrators can easily identify which User is linked to which Employee directly from the Users list view.

---

## 🔗 Create and Link Employee from User

### Objective
Quickly create and associate an **Employee record** with an existing User account.

### Steps
1. Navigate to **Settings → Users**
2. Open a User record
3. Click **Create Employee** (top-right)

### System Behavior
Odoo automatically creates an Employee record and links it to the selected User.

---

## 📌 Use Case

Linking Users with Employee records is required for:
- Task assignment
- Planning and scheduling
- Attendance tracking
- Timesheet logging

---

## ✅ Summary

Proper user and employee linking in the Construction module ensures:
- Clean separation of duties
- Improved security and accountability
- Streamlined workflows across internal and external stakeholders

All configurations can be completed using **Odoo Studio and the Admin UI**, with **no development or technical expertise required**.

✨ **Tip:** Always validate new role permissions using **test users** before assigning access to real users.
