# Project Sprint Management — Role Based Access Control (RBAC)

---

## 1. Overview

This implementation introduces a **Role Based Access Control (RBAC)** system inside the Project Sprint Management module.

The purpose of this implementation is to restrict task access and ensure that only authorized users can create, edit, or delete tasks based on their assigned role within the project.

This prevents unauthorized users from modifying tasks that do not belong to them and improves project security.

---

## 2. Main Objective

The main objective of this implementation is to:

- Restrict task access based on user roles  
- Allow only authorized users to modify tasks  
- Prevent unauthorized users from accessing restricted tasks  
- Display access errors when invalid users attempt restricted operations  

---

## 3. Roles Implemented

The system checks multiple user roles before allowing task access.

The implemented roles are:

- Administrator  
- Project Members  
- Task Creator  
- Team Lead  
- Tester  
- DevOps  

Each role has specific access permissions.

---

## 4. Administrator Access

Administrator has complete access over all tasks without restrictions.

### Permissions

Administrator can:

- Create any task  
- Edit any task  
- Delete any task  
- Access all projects  

### Workflow

```text
User Login → Check Role → If Administrator → Full Access Granted
```

---

## 5. Project Member Access

Users added as project members can work only inside their assigned projects.

### Permissions

Project Members can:

- Access assigned project  
- Create tasks  
- Edit tasks  
- Delete tasks  

Only within projects where they are assigned.

### Workflow

```text
User Login → Check Project Membership → If Assigned → Access Granted
```

---

## 6. Task Creator Access

The user who creates the task automatically becomes the owner of that task.

### Permissions

Task Creator can:

- Edit own task  
- Update task information  
- Manage own task progress  

### Workflow

```text
User Creates Task → System Stores Creator → User Tries Edit → Ownership Check → Access Granted
```

---

## 7. Team Lead Access

If a Team Lead is assigned to a task, that Team Lead can directly edit the task.

Project membership is not required.

### Permissions

Assigned Team Lead can:

- Edit assigned task  
- Update task details  
- Manage task progress  

### Workflow

```text
Admin Creates Task → Assign Team Lead → Team Lead Login → User Match Check → Access Granted
```

---

## 8. Tester Access

If a Tester is assigned in a task, that Tester can directly access and modify the task.

Project membership is not required.

### Permissions

Assigned Tester can:

- Edit task  
- Update testing progress  
- Manage testing related updates  

### Workflow

```text
Admin Creates Task → Assign Tester → Tester Login → User Match Check → Access Granted
```

---

## 9. DevOps Access

DevOps access works similar to Tester access.

If DevOps is assigned to a task, direct task access is allowed.

Project membership is not required.

### Permissions

Assigned DevOps can:

- Edit task  
- Manage deployment related updates  
- Update task progress  

### Workflow

```text
Admin Creates Task → Assign DevOps → DevOps Login → User Match Check → Access Granted
```

---

## 10. Access Restriction Logic

Before allowing task modification, the system validates whether the logged-in user belongs to any authorized role.

Access is allowed if user is:

- Administrator  
- Project Member  
- Task Creator  
- Assigned Team Lead  
- Assigned Tester  
- Assigned DevOps  

If user matches any condition:

**Access Granted**

Otherwise:

**Access Denied**

---

## 11. Protected Operations

Role checking is applied during important task operations.

Protected operations include:

### Task Creation

System checks whether user has permission to create tasks.

### Task Editing

System checks user role before allowing updates.

### Task Deletion

System checks permissions before deletion.

---

## 12. Unauthorized User Restriction

If a user does not belong to any authorized role, the system blocks the operation.

### Example Restriction

If user is not:

- Administrator  
- Project Member  
- Task Creator  
- Assigned Team Lead  
- Assigned Tester  
- Assigned DevOps  

Then:

```text
User Tries Edit → Permission Check Failed → Access Denied → Error Displayed
```

Example Error:

```text
You do not have permission to edit tasks in this project
```

---

## 13. Complete Access Flow

```text
Task Created
      ↓
User Attempts Task Modification
      ↓
Check 1 → Administrator ?
      ↓
Check 2 → Project Member ?
      ↓
Check 3 → Task Creator ?
      ↓
Check 4 → Assigned Team Lead ?
      ↓
Check 5 → Assigned Tester ?
      ↓
Check 6 → Assigned DevOps ?
      ↓
If Matched → Access Granted
      ↓
If No Match → Access Denied
```

---

## 14. Final Working Logic

The RBAC system ensures task access is restricted only to authorized users.

The system automatically validates user permissions whenever someone attempts to:

- Create task  
- Edit task  
- Delete task  

Only valid users can perform actions.

All unauthorized users are blocked automatically.

---

## 15. Result Achieved

Successfully implemented secure Role Based Access Control for project tasks.

### Benefits

- Better security  
- Controlled task ownership  
- Restricted unauthorized access  
- Role based task management  
- Professional workflow management  
- Better team responsibility control  

---

## 16. Conclusion

The implemented Role Based Access Control system improves project security by restricting task access only to authorized users based on their assigned role.

By validating permissions during task operations, the system prevents unauthorized modifications and ensures structured task ownership, creating a secure and enterprise-level project management workflow.
