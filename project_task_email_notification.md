# Odoo 19 Project Module Documentation
### Task Management, User Assignment & Email Notification Setup

## Overview

This document explains the process of creating a task, assigning it to a user, and how the assigned user receives an email notification in the Odoo 19 Project Module.

---

## Objective

- Create tasks in the Project module  
- Assign tasks to users  
- Notify users via email automatically  

---

## Pre-requisite

### Outgoing Mail Server Configuration

Navigate to:

Settings → Technical → Email → Outgoing Mail Servers

Configure the following:

| Field                  | Value                |
|-----------------------|---------------------|
| SMTP Server           | smtp.gmail.com      |
| Port                  | 587                 |
| Encryption            | TLS                 |
| Username              | yourgmail@gmail.com |
| Password              | App Password        |

> Note: Without this configuration, email notifications will not be sent.

---

## Process Flow

Create Task → Assign User → Save Task → Email Sent → User Receives Notification

---

## Step-by-Step Process

### 1. Create Task

Go to:

Project → Projects → Select Project

- Click **New Task**
- Enter Task Name (e.g., POS Setup)
- Add Description (optional)
- Set Deadline
- Click **Save**

---

### 2. Assign User

- Open the created task  
- In **Assigned To** field, select the user  
- Click **Save**

---

### 3. Email Notification Trigger

- When the task is assigned and saved:
  - Odoo automatically sends an email notification to the assigned user  

---

## Email Notification Details

The user will receive an email containing:

- Task Name  
- Project Name  
- Deadline  
- Direct link to the task  

---

## System Behavior

- Assigned user becomes responsible for the task  
- Task appears in the user dashboard  
- Email notification is sent automatically  
- Task progress can be tracked using stages  

---

## Example

| Step | Action |
|------|--------|
| 1 | Task "Inventory Setup" created |
| 2 | Assigned to user "Ram" |
| 3 | Task saved |
| 4 | Email sent automatically |
| 5 | User receives notification |

---

## Conclusion

This process ensures that tasks are properly assigned and users are notified via email, enabling effective task management and tracking.

---

## Summary

Create a task, assign it to a user, and Odoo automatically sends an email notification to the assigned user.
