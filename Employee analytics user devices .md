# Employee Analytics: User Devices

**Module:** Employee Analytics Dashboard (Odoo 19)

---

## 1. Overview

The **User Devices** feature shows which devices an employee is logged in from, so admins can keep track of who is accessing Odoo and from where.

It uses the same data as Odoo's own "All User Devices" screen, but presents it inside the Employee Analytics dashboard. It is **view-only**: nobody can revoke a device from this page.

---

## 2. Who can see what

| Role | What they can see |
|---|---|
| **Administrator** | Every user's devices, from the sidebar **Devices** item, and any employee's **Devices** tab |
| **HR / Project Manager** | Any employee's **Devices** tab |
| **Employee** | Only their own devices, on their own **Devices** tab |

The sidebar **Devices** item is shown to the Administrator only. Employees never see it.

---

## 3. Steps for the Administrator

### A. See all users' devices at once
1. Open **Employee Analytics**.
2. In the left sidebar, click **Devices**.
3. The list is grouped by user. Click a user's name to expand their devices.
4. Use the search bar to find a specific user, device or IP address.

### B. See one employee's devices
1. Open **Employee Analytics → Dashboard**.
2. Click the employee's card.
3. Open the **Devices** tab (after GitHub).
4. The table lists that employee's devices.

---

## 4. Steps for an Employee

1. Open **Employee Analytics → Dashboard**.
2. Click your own card.
3. Open the **Devices** tab.
4. You see the devices that are logged in to your account.

Employees can open only their own page, so they cannot see anyone else's name or devices.

---

## 5. What the table shows

| Column | Meaning |
|---|---|
| **User** | Name of the account the device belongs to |
| **Device** | Operating system and browser, for example *Windows Chrome* |
| **IP Address** | Address the device connected from |
| **Location** | City and country, shown as `-` when unknown |
| **First Activity** | When the device first logged in |
| **Last Activity** | The most recent time the device was used |
| **Status** | See below |

The header shows a summary such as *"2 active of 2 device(s)"*.

### Status values
| Status | Meaning |
|---|---|
| **Current** | The device being used right now |
| **Active** | A logged-in device that has not been revoked |
| **Revoked** | A device whose access has been removed |

---

## 6. Good to know

- **View-only.** The tab has no revoke or edit option. Revoking is done separately by the administrator in Odoo's own settings.
- **Needs a linked user.** If an employee has no **Related User** on their employee record, the tab shows *"This employee isn't linked to a user account, so there are no devices."*
- **Times** are shown in your own timezone.
- **Location** may show `-` for local or internal IP addresses (for example 127.0.0.1 or 10.x.x.x).

---

## 7. Troubleshooting

| Problem | What to check |
|---|---|
| The **Devices** item is missing in the sidebar | It appears for the Administrator only. Also refresh the browser with **Ctrl+Shift+R**. |
| The **Devices** tab is missing on an employee | Refresh the browser with **Ctrl+Shift+R** after an update. |
| "Isn't linked to a user account" message | Set the **Related User** on the employee's form. |
| An employee sees only one device | Employees see only their own account's devices. Check the device is logged in with that account. |
| The employee page shows an access error | An employee can open only their own page. |

---

## 8. Quick checklist

- [ ] Administrator sees **Devices** in the sidebar.
- [ ] Employees do not see **Devices** in the sidebar.
- [ ] The **Devices** tab shows the user's name, device, IP, location, activity times and status.
- [ ] An employee sees only their own devices.
- [ ] No revoke or "Open in Odoo" option appears on the tab.
