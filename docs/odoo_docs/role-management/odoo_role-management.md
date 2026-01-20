# Odoo Access Rights & User Permissions – Detailed Guide

## 1. What Are Access Rights in Odoo?

Access rights control:
- Which **applications** a user can see  
- Which **records** a user can view  
- What **actions** a user can perform:
  - **Create**
  - **Read**
  - **Update (Write)**
  - **Delete**

### Purpose of Access Rights
- Ensure users only see what they need  
- Protect sensitive data  
- Prevent accidental data loss  

### Key Components
Access rights in Odoo are managed through:
- **Users**  
- **Groups**  
- **Access Control Lists (ACLs)**  
- **Record Rules**

> 🔐 **Important Rule**: Only users with **Administrator** permissions can change access rights.

---

## 2. Why Access Rights Must Be Handled Carefully

Incorrect changes can:
- Lock **all administrators** out of settings  
- Prevent users from accessing **critical data**  
- Break **business workflows**

### ⚠️ “Impotent Admin” Risk
- No user can modify access rights  
- Recovery is **impossible without Odoo Support**

> ✅ **Strong Recommendation**:  
> - Always **test changes on a staging/test database**  
> - Consult an **Odoo Business Analyst** or **Odoo Support** before major changes

---

## 3. Granting Administrator Access to a User

### Step-by-Step: Make a User an Administrator
1. Go to **Settings** app  
2. Click **Manage Users**  
3. Select a user  
4. Open the **Access Rights** tab  
5. Scroll to **Administration** section  
6. Set **Administration** to:  
   → **Access Rights**  
7. Click **Save**

✅ The user can now **manage access rights** for other users.

> ℹ️ A user without this permission **cannot modify other users**, even if they are a manager.

---

## 4. Managing Access Rights for a User

### Step-by-Step: Edit User Permissions
1. Go to **Settings → Manage Users**  
2. Select the user  
3. Open the **Access Rights** tab  
4. Review each application section  
5. For each app, choose a permission level:
   - **None / Blank** – No access  
   - **User: Own Documents** – Only their records  
   - **User: All Documents** – All records  
   - **Administrator** – Full control  

### Example: Sales App
| Role           | Permission Level         |
|----------------|--------------------------|
| Salesperson    | User: Own Documents      |
| Sales Manager  | User: All Documents      |
| Sales Admin    | Administrator            |

---

## 5. Administration Permission Levels Explained

| Option         | Meaning                                                  |
|----------------|----------------------------------------------------------|
| **Settings**   | Can access settings but **cannot modify access rights**  |
| **Access Rights** | **Full control** over users, groups, and permissions |

> 🔐 Only users with **Access Rights** can modify security settings.

---

## 6. Managing Specific Permissions (Advanced Control)

Sometimes, bundled permissions are insufficient.

### Example Use Case
A **payroll administrator**:
- Needs full access to **Timesheets**  
- Should **not** submit their **own** timesheets  

> ✅ **Developer Mode is required** for fine-grained control.

---

## 7. Enable Developer Mode

### Steps
1. Go to **Settings**  
2. Scroll to the bottom  
3. Click **Activate Developer Mode**

✅ Advanced security options (e.g., Technical Access Rights, Groups) become visible.

---

## 8. Technical Access Rights (Groups & Inheritance)

### Step-by-Step: Access Technical Permissions
1. Go to **Settings → Manage Users**  
2. Select a user  
3. Open **Technical Access Rights** tab  

#### Two Key Sections:
- **A. Selected Groups**: Explicit permissions assigned  
- **B. Groups Added Automatically**: Permissions inherited (cannot be removed manually)

---

## 9. Understanding Group Inheritance

### Example
If a user is assigned:  
→ **Sales / Administrator**

Odoo **automatically adds**:
- Website / Restricted Editor  
- Canned Responses Administrator  

### Why?
- Ensures **required dependencies**  
- Prevents **permission conflicts**

---

## 10. Adding or Removing Group Permissions

### To Add a Permission
1. Click **Add a line** in **Selected Groups**  
2. Choose the required group  
3. Click **Save**

### To Remove a Permission
1. Click **❌** next to the group  
2. Click **Save**

> ⚠️ Removing groups may **automatically remove inherited permissions**.

---

## 11. Color Indicators in Technical Permissions

| Color / Style | Meaning                              |
|---------------|--------------------------------------|
| **Green**     | Permission already provided by another group |
| **Red**       | Conflicting permissions              |
| *Italic*      | Implied permissions (auto-inherited) |

---

## 12. Creating or Modifying Groups

Groups are **reusable permission sets** for multiple users.

### Step-by-Step: Access Groups
1. Enable **Developer Mode**  
2. Go to **Settings → Users & Companies → Groups**

---

## 13. Creating a New Group

1. Click **Create**  
2. Enter:
   - **Group Name**  
   - **Application**  
   - (Optional) **Enable Share Group**  
3. Click **Save**

> ✅ Always **test new groups** using test users.

---

## 14. Group Configuration Tabs Explained

### **Users Tab**
- Lists users in the group  
  - **Black text** → Admin users  
  - **Blue text** → Regular users  

### **Inherited Tab**
- Shows groups **automatically inherited**  
- 📌 Example:  
  If `Sales/Admin` inherits `Website/Editor`, all sales admins become website editors.

### **Menus Tab**
- Controls **menu visibility** for the group

### **Views Tab**
- Restricts access to specific **views** (Form, List, Kanban)

### **Access Rights Tab (Model-Level Security)**
Defines **CRUD** permissions:

| Permission | Meaning             |
|-----------|---------------------|
| **Read**  | View records        |
| **Write** | Edit records        |
| **Create**| Create new records  |
| **Delete**| Delete records      |

> 📌 **Naming Best Practice**:  
> Use structured names like `res.partner.purchase.manager`

---

## 15. Record Rules (Row-Level Security)

Record Rules refine access at the **data level** using **domains** (filters).

### Example Domain
```python
[('user_id', '=', user.id)]

## 16. Superuser Mode (Emergency Access)

**Superuser mode**:
- Bypasses **all access rights** and **record rules**

### Activate Superuser Mode
1. Enable **Developer Mode**  
2. Click the 🐞 **Debug** icon (usually in the top-right corner)  
3. Select **Become Superuser**

---

## 17. Risks of Superuser Mode

> ⚠️ **Very Dangerous if Misused**

- Can **break access control**  
- Can **lock out all administrators**  
- Applies **no restrictions** on changes  

✅ **Use only for debugging** and **exit immediately** after troubleshooting.

---

## 18. Exit Superuser Mode Safely

1. Click your **profile name** (top-right corner)  
2. Click **Log out**  
3. **Log back in normally** to return to your regular user session