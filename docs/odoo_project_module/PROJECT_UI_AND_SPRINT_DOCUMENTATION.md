# 🚀 Project UI & Sprint Management – Odoo 19

## 📌 Overview

This document describes the custom UI developed for the Odoo 19 Project Module.

The system provides a **Jira-like project management experience** with:
- Project Dashboard
- Task Management (List + Kanban)
- Sprint Management
- Progress Tracking

---

# 📊 Project Dashboard

## 🧭 Header Section

- Project Name (e.g., Agno Project)
- Status Indicator (On Track / At Risk)
- Circular Progress Indicator (e.g., 25% Done)

---

## 📈 Key Metrics

- Total Tasks
- In Progress
- Completed
- Overdue

---

## 📉 Overall Progress

- Visual progress bar
- Based on:
  - Done
  - In Progress
  - Pending

---

## 🔍 Actions & Search

- Search by:
  - Task name
  - Stage
  - Assignee
  - Tags

- Actions:
  - ➕ New Task
  - 📂 Open Board

---

# 📋 Task Management Views

The system provides **two types of task views**:

1. 📄 List View (Table)
2. 📌 Kanban View (Board)

Users can switch between these views based on their workflow.

---

## 📄 1. List View (Table View)

### 🧾 Overview

Displays tasks in a structured table format, useful for **analysis and quick tracking**.

---

### 📊 Columns

- **Task Name**
- **Stage**
- **Priority**
- **Deadline**
- **Assignee**
- **Story Points (SP)**
- **Action (Open Task)**

---

### ⚡ Features

- Overdue tasks highlighted in red
- Priority-based visibility
- Compact and data-rich layout
- Easy scanning of all tasks

---

### 🎯 Use Case

- Manager overview
- Deadline tracking
- Team monitoring

---

## 📌 2. Kanban View (Board View)

### 🧭 Overview

Displays tasks as cards grouped by stages, ideal for **visual workflow tracking**.

---

### 📊 Stages

- To Do
- In Progress
- Code Review
- Testing
- Done

---

### 🧾 Task Cards Include

- Task Title
- Priority
- Deadline
- Assignee

---

### ⚡ Features

- Drag & drop support
- Visual task flow
- Easy status updates
- Interactive UI

---

### 🎯 Use Case

- Developer workflow
- Daily task updates
- Sprint execution

---

## 🔄 View Switching

Users can switch between:

- 📄 List View → structured data view  
- 📌 Kanban View → visual workflow  

---

# 🏃 Sprint Management

## 📌 Sprint Overview

- Sprint Name (e.g., sprint-3)
- Status:
  - Draft
  - Active
  - Completed
- Duration (Start → End date)
- Remaining days indicator

---

## 🎯 Sprint Goals

- Define sprint objective
- Editable goal section

---

## 📊 Sprint Metrics

- Total Tasks
- In Progress
- Done
- Pending
- Story Points

---

## 📉 Sprint Progress

- Completion percentage (e.g., 33%)
- Task completion ratio

---

## 📊 Burndown Chart

Tracks:

- Ideal progress
- Actual progress
- Risk level

---

# 📊 Project Summary Panel

Right-side panel includes:

- Project status (On Track)
- Completion percentage
- Task breakdown:
  - Total
  - Done
  - In Progress
  - Overdue

---

# 🕒 Recent Activity

- Displays recent project actions
- Includes:
  - User
  - Activity
  - Timestamp

---

# 🎯 Key Features

- ✅ Modern dashboard UI
- ✅ List + Kanban views
- ✅ Sprint lifecycle management
- ✅ Progress tracking
- ✅ Burndown chart
- ✅ Search & filtering
- ✅ Status indicators

---

# 🚀 Benefits

- Improves visibility of tasks
- Easy deadline tracking
- Supports Agile workflow
- Enhances team productivity

---

# 🔧 Technical Highlights

- Built using Odoo 19
- XML views (Tree, Kanban, Form)
- Custom CSS for UI
- JavaScript for dynamic behavior
- Modular structure

---

# 📌 Future Enhancements

- Notifications for overdue tasks
- Role-based dashboards
- Advanced analytics
- Timesheet integration

---