# Project Sprint Management

### Odoo 19 Module — User & Technical Documentation

*Agile Sprint Management, Task Tracking, Team Collaboration & Reporting*

| Property | Value |
|---|---|
| **Module** | `project_sprint_management` |
| **Version** | 19.0.1.2.0 |
| **License** | LGPL-3 |

## Table of Contents

1. [Module Overview](#1-module-overview)
2. [Module Architecture](#2-module-architecture)
3. [Roles & Permissions](#3-roles--permissions)
4. [Installation & Setup — Step by Step](#4-installation--setup--step-by-step)
5. [User Guide — How to Use Each Feature](#5-user-guide--how-to-use-each-feature)
6. [Administrator Guide](#6-administrator-guide)
7. [Troubleshooting & Known Points to Verify](#7-troubleshooting--known-points-to-verify)
8. [Glossary](#8-glossary)

---

## 1. Module Overview

Project Sprint Management is a custom Odoo 19 module that extends Odoo's built-in Project app with Agile/Scrum-style sprint planning, story points, sprint health tracking, burndown reporting, task-level comments with @mention notifications, additional team-role fields, a redesigned Project Detail workspace, and automated deadline/overdue email notifications.

It is built as an **extension module** — it depends on and inherits from Odoo's standard `project` and `mail` apps rather than replacing them, so all standard Project functionality (stages, kanban, activities, chatter) continues to work alongside the new features.

### 1.1 What This Module Adds

- **Sprint Management** — Create sprints, assign tasks to them, and track progress, velocity, story points and "at risk" health status automatically.
- **Burndown Reporting** — Ideal-vs-actual burndown data generated per sprint for graph and pivot analysis.
- **Enhanced Tasks** — Story points, overdue detection, sprint linkage, testing status, team lead/tech lead fields, and task sizing (T-shirt sizes).
- **Task Comments & @Mentions** — A lightweight comment thread on each task with @username/@email mention autocomplete that emails the mentioned person.
- **Automated Notifications** — Daily scheduled job flags overdue tasks and emails Project Leads/Administrators; deadline-reached notifications alert assignees.
- **Activity Feed on Projects** — Stage changes, priority changes, reassignments, deadline changes and sprint moves are auto-posted to the project's chatter as readable log entries.
- **Redesigned Project Views** — A custom Project Detail page, a grid/kanban project board with Active/Inactive filtering, and Project Lead assignment.
- **Role-Based Access** — Uses Odoo's standard Project User / Project Manager security groups to control who can create, edit or delete sprints, burndown data and comments.

### 1.2 Technical Requirements

| Requirement | Detail |
|---|---|
| Odoo Version | Odoo 19.0 (Community or Enterprise) |
| Module Dependencies | `project` (Odoo Project app), `mail` (Discuss/Chatter/Email) |
| Module Technical Name | `project_sprint_management` |
| Module Version | 19.0.1.2.0 |
| Type | Application (`installable`, `application: True`) |
| License | LGPL-3 |
| Outgoing Mail | A working outgoing mail server must be configured for deadline, overdue and @mention email notifications to send |

> **Note:** This module modifies the standard `project.task` and `project.project` models directly (via `_inherit`). Always test installation/upgrade on a staging database before applying to production.

---

## 2. Module Architecture

The module follows standard Odoo structure. Below is what each part is responsible for.

### 2.1 Data Models

| Model (technical name) | Purpose |
|---|---|
| `project.sprint` | Core Sprint model — name, dates, goal, state, linked tasks, computed progress/velocity/health/story-point metrics |
| `sprint.burndown` | One row per day of a sprint's duration, storing planned/ideal/actual remaining points for the Burndown Chart |
| `project.task.comment` | Lightweight comment thread per task, independent of Odoo chatter, with @mention parsing and attachments |
| `project.task` (extended) | Adds `sprint_id`, `story_points`, overdue tracking, `testing_status`, `team_lead_id`, `tech_lead_id`, `size`, `estimate`, `iteration`, `tester_ids` and more |
| `project.project` (extended) | Adds `project_status` (Active/Inactive) and `lead_ids` (Project Leads), plus a custom "Open Tasks" action |

### 2.2 Views Added

| View / Screen | What It Shows |
|---|---|
| Sprint Board (`action_sprint_tasks`) | Kanban board of tasks scoped to a sprint, grouped by stage |
| Sprints (`action_sprint`) | List/form of all sprints with Start/Complete/Reset actions and metric buttons |
| Burndown Chart / Burndown Data | Graph and list views plotting ideal vs. actual remaining points per day |
| Project Detail (`action_project_detail`) | Custom two-column project workspace opened from a project's "Open Tasks" button |
| Project Kanban Grid | Project board grid/kanban with Active/Inactive status coloring |
| Project Search Filters | "Active Projects" / "Inactive Projects" quick filters on the Projects list |
| Task Form (Sprint tab) | Adds Sprint, Story Points fields to the standard task form |
| Task Form (Comments tab) | Adds the comment thread with @mention input and attachments |
| Task Form (Additional Info tab) | Adds Team Lead, Tech Lead, Tester(s), Size, Estimate, Iteration, Testing Status |

### 2.3 Automated Jobs (Scheduled Actions)

| Cron Job | Frequency | What It Does |
|---|---|---|
| Check Overdue Tasks | Daily | Finds tasks whose End Date has passed and are not Done/Completed; emails Project Leads/Administrators and posts a chatter note |

> **Note:** The module also contains a deadline-reached notification routine (notifies the assignee the day the End Date arrives) and three email templates (Task Created, Deadline Reached, Task Overdue). Only the overdue check is currently registered as a scheduled job in `data/corn.xml` — confirm with your administrator whether the deadline-reached job should also be scheduled, or is intended to be triggered another way.

---

## 3. Roles & Permissions

The module does not introduce new security groups. It attaches its access rules to Odoo's existing Project security groups, so user access follows the roles already assigned in **Settings → Users & Companies → Users**.

| Odoo Group | Sprints | Burndown Data | Task Comments |
|---|---|---|---|
| Project User (`project.group_project_user`) | Read / Write / Create | Read / Write / Create | Read / Write / Create / Delete |
| Project Manager (`project.group_project_manager`) | Read / Write / Create / Delete | Read / Write / Create / Delete | Read / Write / Create / Delete |

- **Project User** — Can create and update sprints and comments, and log burndown data, but cannot delete sprints or burndown records.
- **Project Manager** — Full control, including deleting sprints and burndown history.
- **Project Leads (`lead_ids`)** — A per-project field (not a security group) — the users listed here, plus anyone in the Project Manager / Administrator groups, receive overdue-task email alerts for that project.

---

## 4. Installation & Setup — Step by Step

Follow these stages in order on a staging environment first.

### Stage 1 — Prepare the Environment

1. Confirm the target Odoo instance is running Odoo 19.
2. Confirm the standard Project and Discuss (`mail`) apps are already installed — this module depends on both.
3. Configure an outgoing mail server under **Settings → Technical → Email → Outgoing Mail Servers**, since notifications rely on it.

### Stage 2 — Install the Module

4. Copy the `project_sprint_management` folder into your Odoo add-ons path.
5. Restart the Odoo service so it discovers the new module.
6. Enable Developer Mode (**Settings → General Settings → Activate the developer mode**).
7. Go to **Apps**, click **Update Apps List**, then search for "Project Management" (the module's display name).
8. Click **Install**. Odoo will load the security rules, cron job, email templates, views and static assets automatically.

### Stage 3 — Assign User Roles

9. Go to **Settings → Users & Companies → Users**.
10. For each project team member, open their user record and set the Project access right to **User** or **Manager** as appropriate under the Project section of the Access Rights tab.
11. Open each Project's form and set **Project Leads** (the new Project Leads field) to the people who should receive overdue-task alerts for that project.

### Stage 4 — Verify the Install

12. Open any project and confirm the "Open Tasks" / project detail button loads the new Project Detail page.
13. Open a task and confirm the Sprint, Story Points, Comments and Additional Info tabs appear.
14. Go to **Project → Sprints** and confirm you can create a sprint.
15. Check **Settings → Technical → Automation → Scheduled Actions** for "Check Overdue Tasks" and confirm it is Active.

---

## 5. User Guide — How to Use Each Feature

### 5.1 Creating and Running a Sprint

Sprints are the unit of planning. A task can belong to at most one sprint at a time.

1. Navigate to **Project → Sprints → New**.
2. Enter a unique Sprint Name (duplicate names are blocked), a Start Date, an End Date and a Sprint Goal (description).
3. Save. The sprint is created in **Draft** state.
4. Add tasks to the sprint either from the sprint's Tasks list, or by opening a task and setting its Sprint field.
5. Click **Start Sprint**. This requires both a Start Date and End Date, and the End Date must be after the Start Date; the sprint moves to **Active**.
6. As the team works, move tasks through their kanban stages as usual — the sprint's Progress, Story Points, Velocity and Health fields update automatically.
7. Click **Complete Sprint** when the sprint's timebox ends, moving it to **Completed**. Use **Reset to Draft** if you need to reopen it.

#### What the Sprint Metrics Mean

| Field | Meaning |
|---|---|
| Progress | % of tasks in a Done/Completed/Closed (or folded) stage |
| Story Points Progress | % of story points completed, if any tasks have story points set |
| Velocity (tasks/day) | Completed tasks divided by the sprint's total day count |
| Days Remaining / Total Days | Countdown based on Start/End Date |
| Sprint at Risk | True when under 30% of sprint time remains and progress is under 50% |
| Health | On Track / In Progress / Behind / At Risk, derived from progress and time remaining |

#### Viewing Reports from a Sprint

- Click the **All Tasks / Done Tasks / Pending Tasks / In Progress** smart buttons on the sprint form to jump to a filtered task list.
- Click **View Burndown** to open a graph/pivot of the sprint's tasks grouped by stage.
- The **Burndown Chart** menu shows ideal-vs-actual remaining points per day, generated from the sprint's Start/End Date and current story point totals.

### 5.2 Working with Tasks

1. Open a task from the Project Detail page, the Sprint Board, or the standard Tasks menu.
2. On the **Sprint** tab, set the Sprint and Story Points (Fibonacci values such as 1, 2, 3, 5, 8, 13 are recommended).
3. On the **Additional Info** tab, set Team Lead, Tech Lead, Size (XS–XL), Estimate, Iteration and Tester(s) as needed for your workflow.
4. Assignee(s) (`user_ids`), a Start Date and a Target Date (`date_deadline`) are required before the task can be saved, unless it is a sub-task.
5. Move the task across kanban stages as work progresses; each meaningful change (stage, priority, assignee, deadline, sprint) is automatically posted as a readable note on the parent Project's chatter, so managers can follow activity without opening every task.

> **Note:** A task is treated as "Done" by this module when its stage is folded, or its stage name is `done`, `completed`, or `closed` (case-insensitive). Make sure your kanban stages use one of these names, or mark the final stage as "folded", for progress and overdue logic to work correctly.

### 5.3 Task Comments and @Mentions

1. Open a task and go to the **Comments** tab.
2. Type your comment. Type `@` followed by a name, login or email to bring up the mention autocomplete and select a teammate.
3. Save the comment. If a matching user is found, that person receives an email notification with a link back to the task; if you typed a full email address that doesn't match any user, the email is still sent directly to that address.
4. Attachments can be added to a comment and reopened later via the comment's Attachments button.

> **Note:** Mentions are matched in this order: exact email, then login, then user name. If several users share a similar name, use their login or email in the mention to avoid ambiguity.

### 5.4 Project Detail Workspace

- From any Project, click **Open Tasks** (or the project's card) to open the custom Project Detail page.
- The page presents a KPI banner (task counts, progress) and collapsible kanban columns for the project's stages, with per-column scrolling for large boards.
- Use the project-level **Status** field (Active/Inactive) and the **Active Projects / Inactive Projects** filters on the Projects list to archive projects out of the main board without deleting them.
- Assign one or more **Project Leads** on the project form — they are the people notified when a task in that project becomes overdue.

### 5.5 Notifications You Will Receive

| Notification | Trigger | Recipient |
|---|---|---|
| Task Created | A new task is created with at least one assignee | Assignee(s) |
| Deadline Reached | A task's Target Date arrives and the task is not yet Done | Assignee(s), via email + an Odoo activity |
| Task Overdue | A task's Target Date has passed and it is still not Done (checked daily) | Project Leads, Project Managers and Administrators |
| Mentioned in Comment | Someone @mentions you in a task comment | The mentioned user (or email address) |

---

## 6. Administrator Guide

### 6.1 Managing Access

- Grant **Project → User** for team members who should log time, update tasks, create sprints and comments.
- Grant **Project → Manager (Administrator)** for leads who need to delete sprints/burndown history or manage settings.
- Assign **Project Leads** per project so overdue alerts route to the right people.

### 6.2 Monitoring the Scheduled Job

1. Go to **Settings → Technical → Automation → Scheduled Actions**.
2. Open "Check Overdue Tasks".
3. Confirm it is **Active** and runs every 1 day; use **Run Manually** to test it immediately after setup.

### 6.3 Email Templates

Three templates ship with the module and can be customized under **Settings → Technical → Email → Templates**:

- **Task Created** — sent to new assignees
- **Deadline Reached** — sent the day a task's Target Date arrives
- **Task Overdue (Admin)** — sent to Project Leads/Managers/Admins once a task passes its deadline

---

## 7. Troubleshooting & Known Points to Verify

| Symptom | Likely Cause / What to Check |
|---|---|
| "Target Date is required" when saving a task | Every top-level task (not a sub-task) needs an Assignee, Start Date and Target Date before it can be saved |
| Sprint progress stuck at 0% | Check that your kanban stage names include "done"/"completed"/"closed", or that the final stage is marked Folded |
| No overdue emails arriving | Confirm the outgoing mail server is configured and the "Check Overdue Tasks" scheduled action is Active |
| @Mention email not received | The typed name/login/email did not match an active user, or the user has no email set; try mentioning by exact email |
| Duplicate sprint name error | Sprint names must be unique across the database, not just within one project |
| User can't delete a sprint | Only the Project Manager group has delete rights on sprints and burndown data by design |

---

## 8. Glossary

| Term | Definition |
|---|---|
| Sprint | A fixed time-boxed period (Draft → Active → Completed) used to group and track a batch of tasks |
| Story Points | A relative effort estimate assigned to a task, typically using Fibonacci numbers |
| Velocity | Completed tasks per day within a sprint's duration — a rough throughput indicator |
| Burndown Chart | A day-by-day comparison of ideal vs. actual remaining work in a sprint |
| At Risk | A sprint flagged automatically when time is running low and progress is behind |
| Project Lead | A user assigned on the project record who receives overdue-task alerts |

---

