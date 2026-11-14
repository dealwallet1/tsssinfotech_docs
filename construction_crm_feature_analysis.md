# Construction Builder – CRM Feature Gap Analysis Report

## 1. Executive Summary
- The Construction Builder module does not rebuild CRM. It runs on the standard Odoo CRM app and adds a link from opportunities to construction projects.
- Of standard CRM features, 8 work in the demo and 11 were not shown. The Construction link to CRM is partly built: 3 items work, 4 are partial and 6 are missing.
- The Construction module is the right place for the CRM-to-project link. No other Odoo module is needed. Standard CRM, Sales and Website CRM cover the rest.
- Do not deploy yet. Close the gaps in section 7 first, then test locally.
- The module and demo run on Odoo 19. The missing features are the same in Odoo 19 and 20, so they can be built on 19 now.

## 2. Scope and Method

| Source | How it was used |
|---|---|
| Odoo 20 CRM documentation | Feature list read through search results, because the page blocks direct automated opening. The list matches Odoo 19 plus a Membership / Partnership item. |
| Demo video (9.5 minutes) | Watched and read key screens. No audio. |
| Module source code | Latest commit zip and the full folder zip. Both are identical. The folder has no git history, so branches could not be compared. |

The module was not run, and the standard CRM features were not tested. Results come from reading the code and the video.

## 3. Standard Odoo CRM Features
These are built into Odoo. They are not custom code.

| Area | Feature | Status |
|---|---|---|
| Pipeline | Kanban pipeline with stages | Working |
| Pipeline | Other views (list, calendar, pivot, graph, activity) | Working |
| Pipeline | Lost opportunities and reasons | Not verified |
| Pipeline | Merge similar leads | Not verified |
| Pipeline | Sales teams and assignment rules | Not verified |
| Acquire | Opportunity form | Working |
| Acquire | Quotations and orders from the opportunity | Working |
| Acquire | Leads menu and conversion | Not verified |
| Acquire | Web contact form creating a lead | Not verified |
| Acquire | Email alias creating leads | Not verified |
| Acquire | Lead mining | Not verified |
| Track | Predictive lead scoring | Not verified |
| Track | Lead reports (unattended, quality, attribution) | Not verified |
| Analyze | Reporting menu | Working |
| Analyze | Expected revenue and forecast | Not verified |
| Day-to-day | Chatter and activities | Working |
| Day-to-day | Lead enrichment | Working |
| Day-to-day | Meetings | Working |
| Day-to-day | Activity plans and gamification | Not verified |

**8 working and 11 not verified.** The 11 need a quick test in the CRM settings, not development. Membership / Partnership (new in Odoo 20) is not part of this count.

## 4. The Construction Link to CRM (Custom Code)

| # | Feature | Status | Evidence |
|---:|---|---|---|
| 1 | Opportunity-to-project link (button, smart button, field) | Working | `models/crm.py` |
| 2 | Sales Order field and New Quotation button on the project | Working | `models/project.py`, `models/sale.py` |
| 3 | Chatter and activities on the project | Working | `views/project_views.xml` |
| 4 | Project creation from an opportunity | Partial | Opens a blank form only |
| 5 | Opportunity data copied into the project | Partial | Name, customer and opportunity only. Budget, manager, tags and location are empty. |
| 6 | Sales Order link | Partial | One order only, set only on confirmation |
| 7 | Project views | Partial | Calendar, pivot and graph exist but are not enabled |
| 8 | Duplicate-project guard | Missing | No constraint. The button shows on every stage, including Lost. |
| 9 | Construction fields on the opportunity | Missing | Nothing added to `crm.lead` beyond the project link |
| 10 | Stage and status sync | Missing | No write or stage logic |
| 11 | CRM-to-project report | Missing | Only a worked-hours report exists |
| 12 | Quotation from the project tied to the opportunity | Missing | `action_create_quotation` does not pass the opportunity |
| 13 | Button to create a project from a Sales Order | Missing | Code exists in `models/sale.py`, no button in any view |

The native Odoo Project app is not linked. It is not required for this task.

## 5. Suitability Assessment

| Question | Answer |
|---|---|
| Is the Construction module the right choice? | Yes for the CRM-to-project link. No for general CRM features, which belong to standard Odoo CRM. |
| Is a different module needed? | No. Standard CRM, Sales and Website CRM cover the rest. |
| Is it ready for deployment? | No. Gaps remain in sections 4 and 6. |

## 6. Other Problems Found

| Problem | Impact |
|---|---|
| Every user has full access. The Construction User group exists but is unused, and there are no record rules. | Any user can read and change all construction data. |
| The public website shows customer name, manager and budget for all projects, including drafts. | Customer and budget data is exposed. |
| `sale_crm` is not declared in the manifest. | The opportunity link on orders depends on it. |
| Six data and report files and the wizard are empty and not loaded. | No impact on CRM, but they are unfinished. |


## 7. Suggested Plan

| Phase | Work |
|---|---|
| 1. Safety and data integrity | `sale_crm`, access rules, website privacy, data copy, duplicate guard, quotation link |
| 2. Workflow | Construction fields, stage sync, Sales Order button, multiple orders |
| 3. Reporting and views | Won revenue vs budget report, project views |
| 4. Verify and release | Test the 11 standard CRM features, set up locally on Odoo 19, test, then deploy |

## 8. Future Considerations
- **Upgrade to Odoo 20:** The missing features are the same in 19 and 20. Upgrading is a separate task that needs a database upgrade and a retest of the module. It has not been assessed.
- **Native Project app:** Decide later whether the custom project model should link to Odoo's Project app.
- **Membership / Partnership:** New in Odoo 20 CRM. Review it only if relevant to the business.

