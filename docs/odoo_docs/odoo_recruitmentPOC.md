# Recruitment POC Module Documentation

## 📌 Overview

The Recruitment POC (Proof of Concept) module is a custom Odoo application designed to manage candidate data, provide skill-based insights, and enable chatbot-driven interaction for recruitment processes.

This module demonstrates end-to-end functionality including backend models, frontend UI, and real-time chatbot communication.

---

## 🚀 Features

### 1. Candidate Management

* Store candidate details such as:

  * Name
  * Skills
  * Education
  * Experience
* Form and Kanban views for easy interaction

### 2. Skills Dashboard

* Displays skill-wise candidate distribution
* Enables filtering candidates based on selected skills
* Provides quick insights for recruiters

### 3. RecruitBot Chatbot

* Interactive chatbot integrated into the UI
* Handles user queries dynamically
* Communicates with backend using API calls

### 4. Dynamic UI

* No page reload required
* Smooth user experience
* Auto-scroll and input handling

---

## 🧱 Module Structure

### 📁 Models (`models/`)

* `candidate.py`
  Handles candidate data storage and management

* `education.py`
  Stores educational details of candidates

* `experience.py`
  Manages work experience information

* `chatbot.py`
  Contains chatbot logic and response handling

* `skills_dashboard.py`
  Computes skill-based analytics and dashboard data

---

### 📁 Controllers (`controllers/`)

* `recruitbot.py`
  Acts as an API layer between frontend and backend
  Receives requests from JavaScript and returns responses

---

### 📁 Views (`views/`)

* `candidate_views.xml`
  Candidate form and list views

* `dashboard_views.xml`
  Skills dashboard UI (Kanban view)

* `menu.xml`
  Menu structure for navigation

---

### 📁 Static Files (`static/src/js/`)

* `chatbot.js`
  Frontend logic for chatbot interaction
  Handles:

  * User input
  * Send button click
  * API calls
  * Displaying responses

---

### 📁 Configuration

* `__manifest__.py`
  Module configuration including dependencies and assets

* `security/ir.model.access.csv`
  Access control rules

---

## 🔄 Workflow

### Chatbot Flow

User → Frontend (chatbot.js) → Backend (recruitbot.py) → Chatbot Logic → Response → UI

### Step-by-step:

1. User enters a message in the chatbot UI
2. JavaScript captures the input
3. Request is sent to backend controller
4. Backend processes the request
5. Response is returned to frontend
6. Message is displayed in UI

---

## ⚙️ Technologies Used

* Backend: Python (Odoo ORM)
* Frontend: JavaScript
* UI: XML (Odoo Views)
* Framework: Odoo 19

---

## 🔧 Key Functionalities

### Frontend (JavaScript)

* Event handling (click, keydown)
* Dynamic DOM updates
* Auto-scroll functionality
* API integration

### Backend (Python)

* ORM-based data handling
* Controller routing
* Business logic implementation

---

## 🎯 Outcome

* Efficient candidate data management
* Real-time chatbot interaction
* Skill-based analytics dashboard
* Improved user experience

---

## 🔮 Future Enhancements

* AI-based candidate recommendations
* Resume parsing automation
* Advanced filtering options
* Integration with external job portals

---

## 📌 Conclusion

The Recruitment POC module demonstrates a complete workflow of a recruitment system using Odoo, combining backend logic, frontend interaction, and chatbot integration into a single application.

---

## 💡 One-line Summary

A custom Odoo recruitment module with candidate management, skills dashboard, and chatbot integration.
