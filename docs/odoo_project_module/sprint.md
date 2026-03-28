# Sprint Management (Jira-Style) - Odoo 19

##  Overview
Implemented a Jira-style sprint management system in the Odoo Project module to organize tasks, track progress, and improve team workflow.

---

##  Features

- Sprint model with lifecycle:
  - Planned
  - Active
  - Completed
- Integration with tasks using `sprint_id`
- Sprint board with Kanban view
- Backlog management (tasks without sprint)
- Filtering tasks based on active sprint
- Jira-style UI enhancements (custom kanban design)

---

## 🔄 Sprint Workflow

### 1. Create Sprint
- Navigate to Project → Sprints
- Create a new sprint with:
  - Name
  - Start Date
  - End Date

---

### 2. Add Tasks to Sprint
- Open task
- Assign `sprint_id`
- Tasks without sprint remain in backlog

---

### 3. Start Sprint
- Click **Start Sprint**
- Sprint state changes:


---

### 4. Work on Tasks
- Use Sprint Board (Kanban view)
- Track tasks by stages:
- To Do
- In Progress
- Done

---

### 5. Complete Sprint
- Click **Complete Sprint**
- Sprint state changes:


---

##  System Behavior

- Only **active sprint tasks** are shown in sprint board
- Backlog tasks are handled separately
- Sprint must be started manually (no auto activation)
- Completed sprint becomes read-only (recommended behavior)

---

##  UI Enhancements

- Jira-style Kanban layout
- Custom CSS scoped to:

- Sprint badge displayed on task cards

---

##  Future Improvements

- Story Points system
- Sprint Velocity tracking
- Burndown Chart
- Automatic sprint transitions
- Email notifications for sprint updates