Role-Based Assignment and Field Enhancements in Odoo Project Module

---

## 1. Project Overview

This project extends the default Odoo Project module to implement role-based task assignment and improved task tracking features.

The system ensures that only relevant users (Team Leads and Testers) are selectable, improving task clarity and usability.

---

## 2. Objectives

- Restrict user selection based on roles (Team Lead and Tester)  
- Add additional task tracking fields  
- Improve task form usability  
- Simplify the user interface  

---

## 3. Features Implemented

### 3.1 Role-Based Assignment

- Added Team Lead field  
  - Only users with the Team Lead role are displayed  

- Added Tester field  
  - Only users with the Tester role are displayed  
  - Supports multiple user selection  

---

### 3.2 Employee Role Configuration

- Configured roles in the Employee module:
  - Team Lead  
  - Tester  

- These roles are used to filter users during task assignment  

---

### 3.3 Field Enhancements in Task Page in Project Module

Added new fields to improve task tracking:

- Size (XS to XL)  
- Estimate (effort tracking)  
- Iteration (sprint reference)  
- Start Date  
- Target Date  

These fields help in better planning, estimation, and execution tracking.

---

### 3.4 User Interface Enhancements

- Created an Additional Info section in the task form  

Includes:

- Priority  
- Size  
- Start Date  
- Target Date  
- Tester  

Result:

- Clean and structured layout  
- Improved readability  
- Better organization of task details  

---

### 3.5 UI Simplification

Removed unnecessary elements:

- Priority stars replaced with a dropdown  
- Status button popup removed  
- Deadline field removed  

Reason:

- Status is already managed through Kanban stages  
- Avoid duplication of information  
- Simplify the user interface  

---

## 4. Final Output

- Role-based user selection implemented  
- Clean and simplified user interface  
- Improved task tracking capability  
- Better user experience  

---

## 5. Key Learnings

- Role-based filtering in Odoo  
- Relationship between Employees and Users  
- Form view customization  
- Debugging and fixing UI layout issues  

---

## 6. Conclusion

This implementation enhances the Odoo Project module by introducing role-based assignment and structured task tracking.

It ensures that:

- Only relevant users are assigned to tasks  
- Task information is clear and well organized  
- The user interface remains simple and efficient  

Overall, the system aligns better with real-world team workflows and project management practices.
