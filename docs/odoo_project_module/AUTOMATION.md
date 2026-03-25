 # Automation Rules

- Status = Approved (Code Review) → Stage = Testing
- Status = Approved (Testing) → Stage = Done
- Status = Changes Requested → Stage = In Progress
- Status = Done → Stage = Done

# Overdue Task Alert Automation

## Overview
This feature automatically identifies overdue tasks and notifies the assigned user by creating an activity reminder.

---

## Objective
To ensure that tasks are completed on time by alerting users when deadlines are missed.

---

## Implementation Details

### Model
- Task (`project.task`)

### Trigger
- Based on Date Field

### Date Field Used
- Deadline (`date_deadline`)

### Domain Conditions
- Deadline is less than current date
- Task stage is not Done

```python
[("date_deadline", "<", today), ("stage_id", "not in", done_stage)]

## Notes
Automation reduces manual movement and ensures workflow consistency.
