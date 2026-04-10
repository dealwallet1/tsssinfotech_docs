# Workflow

## Overview

This workflow implements a **Jira-style Agile process** within the Odoo 19 Project module.
It defines a structured lifecycle for tasks, ensuring clarity, accountability, and quality at every stage.

---

## Stages

### 1. Backlog

* Task is created and stored for future planning
* No active work is performed at this stage

### 2. To Do

* Task is reviewed and ready for execution
* Assigned to a developer

### 3. In Progress

* Developer actively works on the task
* Implementation and initial testing are performed

### 4. Code Review

* Reviewer validates:

  * Code quality
  * Logic correctness
  * Best practices
* Feedback is provided if required

### 5. Testing

* Tester verifies:

  * Functional correctness
  * Edge cases
  * Bug-free execution
* Ensures the feature meets requirements

### 6. Done

* Task is fully completed
* Approved by reviewer and tester
* Ready for deployment or delivery

---

## Workflow Flow

**Developer → Reviewer → Tester → Done**

* Developer completes the implementation
* Reviewer checks and approves the code
* Tester validates functionality and stability
* Task is marked as **Done**

---

## Rejection Flow

**Changes Requested → In Progress**

* If issues are identified during review or testing:

  * Task is moved back to **In Progress**
  * Developer reworks based on feedback
  * Process continues until approval

---

## Key Benefits

* Clear ownership at each stage
* Improved code quality and validation
* Reduced production errors
* Better team collaboration and transparency

---

## Notes

* Each stage reflects a specific team responsibility
* Workflow ensures structured delivery and accountability
* Supports scalable Agile practices within Odoo
