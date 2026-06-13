# Task Based Role Access Management

## Overview

This feature provides role-based access control for projects, tasks, sprints, dashboards, and project activities.

Users are assigned responsibilities through project roles such as:

- Project Lead
- Developer
- QA
- DevOps
- Project Member

Role assignments are used for responsibility tracking, reporting, dashboard visibility, and future access control enhancements.

---

## Objective

- Define project responsibilities
- Improve accountability
- Organize team structure
- Enable role-based reporting
- Prepare system for future project-level access control

---

## Supported Roles

### Project Lead

Responsibilities:

- Manage project activities
- Monitor sprint progress
- Review task status
- Coordinate team members

Permissions:

- View project dashboard
- View all project tasks
- View sprint information
- View reports

---

### Developer

Responsibilities:

- Implement assigned tasks
- Update task progress
- Participate in sprint execution

Permissions:

- View assigned tasks
- Update task stages
- Log work progress

---

### QA

Responsibilities:

- Validate completed tasks
- Test implemented features
- Verify bug fixes

Permissions:

- View testing tasks
- Update testing status
- Add testing comments

---

### DevOps

Responsibilities:

- Deployment activities
- Environment management
- Release support

Permissions:

- View deployment tasks
- Update deployment status
- Manage release activities

---

### Project Members

Responsibilities:

- Collaborate on assigned work
- Participate in project execution

Permissions:

- View assigned project information
- View assigned tasks

---

## Project Team Structure

Each project can contain:

- Project Leads
- Developers
- QA Members
- DevOps Members
- Project Members

Example:

Project: Agno Project

Lead:
- Manoj

Developers:
- Vinay
- Raj

QA:
- Teja

DevOps:
- Kiran

Members:
- Additional team members

---

## Dashboard Integration

Role assignments are displayed in:

### Project Overview

- Total Team Members
- Lead Count
- Developer Count
- QA Count
- DevOps Count

### Team Management

Display assigned users by role.

---

## Reporting

Role assignments are used in:

- Project Reports
- Sprint Reports
- Team Utilization Reports
- Resource Allocation Reports

---

## Current Access Behavior

Currently:

- Users with project access can view projects.
- Role assignments define responsibilities only.
- Role assignments do not restrict project visibility.

---

## Future Enhancements

Future versions may support:

### Project Visibility Modes

- Public Project
- Assigned Members Only

When enabled:

- Only assigned Leads
- Developers
- QA Members
- DevOps Members
- Project Members

can access the project.

---

## Acceptance Criteria

- Roles can be assigned per project.
- Multiple users can be assigned to each role.
- Role assignments are displayed correctly.
- Team Management shows assigned members.
- Dashboard displays role statistics.
- Reports use role information.
- Existing project access remains unchanged.