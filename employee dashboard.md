# Employee Analytics Dashboard

### Odoo Module — User Documentation

*Per-employee task and leave analytics, filterable by day, week, month, quarter, year, or a custom date range*

| Property | Value |
|---|---|
| **Module** | `employee_analytics_dashboard` |
| **Version** | 19.0.1.0.0 |
| **License** | LGPL-3 |

## Table of Contents

1. [Overview](#1-overview)
2. [Opening the Dashboard](#2-opening-the-dashboard)
3. [Reading an Employee Card](#3-reading-an-employee-card)
4. [Filtering and Searching](#4-filtering-and-searching)
5. [Viewing an Employee's Full Detail](#5-viewing-an-employees-full-detail)
6. [Exporting the Dashboard](#6-exporting-the-dashboard)
7. [Using the Sidebar](#7-using-the-sidebar)
8. [Who Can See What](#8-who-can-see-what)
9. [Quick Reference](#9-quick-reference)

---

## 1. Overview

The Employee Analytics Dashboard gives managers a single screen with one card per employee, showing their task workload and leave usage. All numbers are calculated live from the Project and Time Off apps and can be narrowed down to a day, week, month, quarter, year, all time, or any custom date range.

This document explains, step by step, how each feature works — for anyone reviewing or using the dashboard day to day.

### What the Dashboard Shows

- An employee card for every active employee, with photo, name, designation and department.
- Total, Pending, In Progress, Done and Overdue task counts per employee, for the selected time period.
- Leaves Taken (approved Time Off days) within the selected period.
- A detail page per employee with five tabs: Overview, Tasks, Projects, Leave and Activity.
- Filters for time period, department and project, plus a search box.
- One-click export of the current view to CSV, Excel or PDF.
- A left-hand sidebar linking to the underlying Employees, Tasks, Leaves, Reports and Departments screens.

---

## 2. Opening the Dashboard

1. Log in to Odoo with your usual account.
2. In the top app menu, click **Employee Analytics**, then **Dashboard**.
3. The dashboard fetches live data for the current month by default and displays one card per employee.

> **Note:** What you see depends on your role — see [Section 8](#8-who-can-see-what) for details.

---

## 3. Reading an Employee Card

Each card summarizes one employee's workload for the currently selected time period:

| Field | What It Shows |
|---|---|
| Photo & Name | Employee's profile picture and full name. |
| Designation | Job title, or the position from the Job Position field if no title is set. |
| Department | The employee's department. |
| Total | Number of tasks assigned to them within the selected period. |
| Pending | Tasks still in a To Do / backlog-style stage. |
| In Progress | Tasks in a Doing / Working / Review / Testing style stage. |
| Done | Tasks in a Done / Completed / Closed stage. |
| Overdue | Tasks not yet done whose deadline has already passed. |
| Leaves Taken | Approved Time Off days that fall inside the selected period. |

> **Note:** Clicking directly on the Total, Pending, In Progress, Done or Overdue number opens that employee's matching tasks in the standard Project Tasks screen. Clicking "Leaves Taken" opens their matching leave requests in Time Off. If there is nothing to show for the period, the dashboard tells you instead of opening an empty screen.

---

## 4. Filtering and Searching

### 4.1 Changing the Time Period

1. Click the period selector near the top of the dashboard (it shows the currently selected period, e.g. "Month").
2. Choose Day, Week, Month, Quarter, Year, All, or "Custom range" from the list.
3. If you choose Custom range, pick a Start Date and an End Date, then confirm. The dashboard reloads with data limited to exactly that window.

| Option | Shows Data For |
|---|---|
| Day | Today only. |
| Week | The current calendar week (Monday–Sunday). |
| Month | The current calendar month. This is the default when the dashboard opens. |
| Quarter | The current calendar quarter. |
| Year | The current calendar year. |
| All | Every record ever created, with no date limit. |
| Custom range | Any specific Start Date / End Date you pick yourself. |

### 4.2 Filtering by Department or Project

- Click the **Department** dropdown and choose a department to show only employees in that department, or choose "All" to clear it.
- Click the **Project** dropdown and choose a project to only count tasks belonging to that project when calculating each employee's numbers.

### 4.3 Searching for an Employee

1. Type part of an employee's name or designation into the search box at the top of the dashboard.
2. The card grid narrows down to matching employees as you type.

### 4.4 Sorting and "Has Work Only"

- Click a column header (where available) to sort the employee list by that value, ascending or descending.
- Use the "Has work" toggle to hide employees with no tasks at all in the selected period, which is useful for quickly spotting idle capacity.

---

## 5. Viewing an Employee's Full Detail

1. Click on an employee's card (or their name/photo) to open their detail page.
2. Browse the five tabs: Overview, Tasks, Projects, Leave and Activity.

### What Each Tab Shows

- **Overview** — the same summary numbers as the card, plus a preview of their 5 most recent tasks.
- **Tasks** — the full list of tasks for the selected period, with project, stage and deadline, and an Overdue/Pending/Active/Done badge on each.
- **Projects** — a per-project breakdown of the same task counts, so you can see which project an employee is busiest on.
- **Leave** — every approved leave request in the selected period, with type and dates.
- **Activity** — a combined, most-recent-first feed of task and leave activity, grouped into Recent Tasks, Active, Pending, Completed, Overdue and Leaves, capped at 5 items per group.

Use the back/close control to return to the main card grid.

---

## 6. Exporting the Dashboard

1. Click the **Export** button/control near the top of the dashboard.
2. Choose a format: **CSV**, **Excel**, or **PDF**.
3. Your browser downloads the file. It reflects exactly what's on screen — the same employees and numbers currently shown after your period, department, project and search filters are applied.

> **Note:** Export always matches your current filters, so narrow the view first (e.g. one department, this month) if you only want that slice in the file.

---

## 7. Using the Sidebar

The left-hand sidebar gives quick access to the standard Odoo screens behind the dashboard's numbers:

| Menu Item | Opens |
|---|---|
| Dashboard | Returns to the main card view (this is the default screen). |
| Employees | The standard Odoo Employees list/kanban/form screens. |
| Tasks | Every project task counted by the dashboard, in the standard Tasks screen. |
| Leaves | Every Time Off request, in the standard Leaves screen. |
| Reports | A pivot/graph view of the same tasks, grouped by assignee and stage. |
| Configuration | The Departments list, which feeds the Department filter on the dashboard. |

---

## 8. Who Can See What

| Role | What They See |
|---|---|
| HR Manager or Project Manager | Every employee's card and detail page. |
| Everyone else | Only their own employee card and detail page — the dashboard automatically restricts the data, they don't need to filter for it. |

> **Note:** This is enforced automatically by the system, not just hidden in the interface — a non-manager cannot pull another employee's tasks, leaves, or detail page even by other means.

---

## 9. Quick Reference

- Open the dashboard: **Employee Analytics → Dashboard**
- Change time period: period selector, top of the dashboard
- Filter by department/project: Department / Project dropdowns
- See an employee's full detail: click their card
- Jump to matching tasks/leaves: click a number on the card
- Export the current view: Export button → CSV / Excel / PDF
- Underlying data screens: sidebar → Employees / Tasks / Leaves / Reports / Configuration

---

*— End of Document —*
