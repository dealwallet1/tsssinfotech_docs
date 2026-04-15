#  Odoo Recruitment POC – Changes & Enhancements

---

##  Dashboard UI Enhancements

###  Overview
- The Recruitment Dashboard UI has been enhanced to improve usability, interactivity, and visual appeal.
- Multiple components such as navigation buttons, filters, and panels were redesigned with better styling and user experience.

---

##  Navigation Bar Improvements

###  Description
The top navigation bar includes the following buttons:
- Dashboard
- Candidates
- Analytics
- Reports

###  Enhancements Implemented
- Updated background colors for all navigation buttons
- Added hover effects using `onmouseover` and `onmouseout`
- Improved button visibility and spacing

###  Result
- Interactive navigation
- Better user experience
- Clear visual feedback on hover

---

##  Skill Filter (Intelligent Filters) Enhancements

###  Description
The Skill Quick Filter section allows users to filter candidates based on skills such as:
- Python
- Java
- JavaScript
- C#
- React
- Angular
- Node.js
- Django
- SQL

###  Enhancements Implemented
- Customized background colors for each skill card
- Improved card design with better UI styling
- Enhanced visual differentiation between skills

###  Result
- Easy identification of skills
- Improved filtering experience
- More attractive UI

---

##  Overview Panel Enhancements

###  Description
The Overview section displays key metrics:
- Total Candidates
- Experienced Candidates
- Freshers
- Skills Mapped

###  Enhancements Implemented
- Updated background colors for overview cards
- Improved alignment and spacing
- Enhanced readability

###  Result
- Clear data visibility
- Better dashboard insights

---

##  Navigation Panel Enhancements

###  Description
The left-side navigation panel includes:
- All Candidates
- Skills Browser
- Location Report
- Experience Report

###  Enhancements Implemented
- Updated background styling
- Improved layout consistency
- Better visual grouping

###  Result
- Easier navigation
- Clean UI structure

---

##  Pro Tip Section Enhancements

###  Description
The Pro Tip section provides helpful insights to users.

###  Enhancements Implemented
- Updated background color
- Improved visibility and highlighting

###  Result
- Better user guidance
- Highlighted important information

---

##  Analytics Section Enhancements

###  Description
The Analytics section is used for visualizing recruitment data.

###  Enhancements Implemented
- Updated background design
- Improved UI consistency with dashboard theme

###  Result
- Better data presentation
- Consistent user experience

---

##  Recruitment POC – Resume Extraction Improvements

###  Changes Done
- Fixed Board/University incorrect extraction issue
- Added strict prompt rules to avoid AI guessing skills/tools
- Improved education parsing logic
- Prevented invalid values like branch names (CSE, ECE) in university field
- Ensured only valid university names are extracted
- Fixed indentation and variable scope errors
- Removed duplicate and incorrect education records creation

###  Prompt Enhancements
- Added strict instruction: Do NOT guess skills/tools
- Ensured only resume-present data is extracted
- Improved university extraction rules (e.g., Krishna University issue fixed)

###  Code Fixes
- Fixed `NameError: data is not defined`
- Fixed `educations not defined` issue
- Corrected indentation issues
- Ensured cleaned `board_university` value is stored properly

###  Result
- Accurate education data extraction
- No unwanted AI-generated values
- Stable module without server errors

---

##  Candidate Resume Selection – Email Notification

###  Overview
When a candidate's resume is **selected** by the recruiter, an automated email notification is triggered and sent to the candidate's registered email address. This keeps the candidate informed about their application status in real time.

---

###  How It Works

1. Recruiter reviews and **selects** a candidate's resume from the Recruitment Dashboard.
2. The system detects the status change (e.g., stage moved to **"Selected"** or equivalent).
3. An automated email is triggered via **Odoo's Email Template** engine.
4. The candidate receives the email at their registered email address.

---

###  Email Configuration Steps

Follow the steps below to configure the email notification for resume selection:

---

####  Step 1: Configure Outgoing Mail Server

> **Path:** `Settings → Technical → Email → Outgoing Mail Servers`

1. Go to **Settings** in Odoo.
2. Navigate to **Technical → Email → Outgoing Mail Servers**.
3. Click **Create** or select an existing server.
4. Fill in the following details:

| Field | Value |
|---|---|
| Description | SMTP Server (e.g., Gmail / Company SMTP) |
| SMTP Server | `smtp.gmail.com` *(or your company SMTP host)* |
| SMTP Port | `587` *(TLS)* or `465` *(SSL)* |
| Connection Security | `TLS (STARTTLS)` or `SSL/TLS` |
| Username | Your email address (e.g., `hr@company.com`) |
| Password | App password or SMTP password |

5. Click **Test Connection** to verify.
6. Click **Save**.

---

####  Step 2: Create or Update the Email Template

> **Path:** `Settings → Technical → Email → Templates`

1. Go to **Settings → Technical → Email → Templates**.
2. Search for an existing **Recruitment** template or click **Create**.
3. Fill in the following fields:

| Field | Value |
|---|---|
| Name | `Candidate Resume Selected Notification` |
| Applies To | `hr.applicant` *(Recruitment Application model)* |
| From | `{{ object.company_id.email }}` or your HR email |
| To (Email) | `{{ object.partner_name }}` or `{{ object.email_from }}` |
| Subject | `Congratulations! Your Resume has been Selected` |

4. In the **Body** tab, write your email content. Example:

```
Dear {{ object.partner_name }},

We are pleased to inform you that your resume has been reviewed 
and you have been selected for the next stage of our recruitment process 
for the position of {{ object.job_id.name }}.

Our team will contact you shortly with further details.

Best Regards,
{{ object.company_id.name }} – HR Team
```

5. Click **Save**.

---

####  Step 3: Link Email Template to Recruitment Stage

> **Path:** `Recruitment → Configuration → Stages`

1. Go to **Recruitment** module.
2. Navigate to **Configuration → Stages**.
3. Open the **"Selected"** stage (or create one if not present).
4. In the **Email Template** field, select:
   - `Candidate Resume Selected Notification` *(template created in Step 2)*
5. Enable **"Send an Email"** toggle if available.
6. Click **Save**.

>  **Note:**

---

####  Step 4: Verify Candidate Email Address

Before testing, ensure the candidate's email is correctly stored:

1. Go to **Recruitment → Candidates**.
2. Open the candidate profile.
3. Confirm the **Email** field is populated correctly.

---

####  Step 5: Test the Email Trigger

1. Open any candidate application from the Recruitment Dashboard.
2. Move the application to the **"Selected"** stage (drag & drop on Kanban or change stage in form view).
3. Verify that the email is sent:
   - Check **Chatter** (bottom of application form) for the email log.
   - Check the candidate's inbox for the received email.

---

###  Email Trigger Flow Diagram

```
Resume Uploaded → Recruiter Reviews → Stage Changed to "Selected"
        ↓
Odoo Detects Stage Change
        ↓
Email Template Triggered (hr.applicant model)
        ↓
Email Sent to Candidate Email Address
        ↓
Candidate Receives Notification 
```

---

###  Troubleshooting

| Issue | Solution |
|---|---|
| Email not sent | Check Outgoing Mail Server configuration and test connection |
| Email goes to spam | Configure SPF/DKIM records for your domain |
| Wrong candidate email | Verify email field in candidate profile |
| Template not triggered | Ensure template is linked to the correct stage |
| SMTP authentication error | Use App Password (for Gmail, enable 2FA and generate App Password) |

---

###  Result
- Candidate is automatically notified upon resume selection
- No manual email effort required from the recruiter
- Professional and consistent communication

---

##  Technical Implementation

###  Technologies Used
| Technology | Purpose |
|---|---|
| Odoo 19 | Base platform |
| XML | UI customization |
| CSS | Styling and background changes |
| JavaScript | Hover effects (`onmouseover`, `onmouseout`) |
| Odoo Email Templates | Automated email notifications |
| SMTP | Email delivery configuration |

###  Key Features
- Background color customization
- Hover effects using `onmouseover` and `onmouseout`
- Responsive UI improvements
- Automated candidate email notification on resume selection

---

##  Conclusion
- These enhancements significantly improve the overall user experience by making the dashboard more interactive, visually appealing, and easy to use.
- The added styling and hover effects provide better feedback and usability for end users.
- The automated email notification ensures candidates are kept informed in real time when their resume is selected, reducing manual communication overhead for the HR team.
