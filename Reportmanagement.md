**Bug -1** 
**Title**
API Reports Dashboard Displays “no available server” Blank Page Without Error Handling

**Description:**
While accessing the API Reports application (apireports.dealwallet.com), the page displays a blank white screen with the message:

no available server

The application fails to load any UI components, dashboard content, or fallback error handling screen.


**Steps to Reproduce:**

1. Open apireports.dealwallet.com
2. Wait for the application to load
3. Observe the displayed page

**Expected Result:**

1. Application should load successfully
2. If backend/server is unavailable, a proper error page or maintenance message should be displayed
3. User should receive meaningful feedback with retry/support options


**Actual Result:**

1. Blank white page is displayed
2. Only raw text message no available server appears
3. No proper UI error handling or recovery option is shown

**Impact:**
Users are unable to access the reports application or perform any actions.



**Bug -2** 
**Title**
Dashboard API returning 404 error – data not loading in production

The Dashboard Overview page in the production environment is failing to load data due to a 404 (Not Found) error from the API.

An error message is displayed:

"Failed to load data: Request failed: 404"

**Because of this:**

1. Revenue Performance chart is not rendered
2. KPI metrics (Total Revenue, Active Users, Avg Churn Rate) are empty
3. Dashboard is partially unusable

**Steps to Reproduce:**

1. Open the production URL (vpnreport.dealwallet.com)
2. Navigate to Dashboard
3. Observe the error message at the top
4. Check that charts and metrics are not loading

**Expected Behavior:**

1. Dashboard API should return valid data
2. Charts and KPI metrics should be displayed correctly

**Actual Behavior:**

1. API request fails with 404 Not Found
2. No data is rendered on the dashboard


**Bug -3** 
**Title**
MobileAdmin section tabs ,Support & Settings are clickable but should have no action in VPNReport Dashboard

**Description**
In the VPNReport dashboard, under the MobileAdmin section, the Support and Settings tabs are currently clickable. However, these tabs are not supposed to perform any action.


**Steps to Reproduce:**

1. Login to VPNReport dashboard
2. Navigate to MobileAdmin section
3. Click on Support tab
4. Click on Settings tab



**Actual Behavior:**

Both tabs are clickable and allow user interaction (triggering navigation or response).


**Bug -4** 
**Title**
Chart Assistant shows "Backend offline" error and fails to respond

**Description**
In the Chart Explorer Gallery page, the Chart Assistant panel is displaying a "Backend offline" error message and is not functioning as expected.

When the user tries to interact with the assistant, it does not process queries and shows the message:
"Backend offline. Check http://127.0.0.1:8000
"

This indicates that the frontend is unable to connect to the backend service.

**Steps to Reproduce:**

1. Navigate to the Chart Explorer page
2. Observe the Chart Assistant panel on the right side
3. Try to interact or send a message (if input is enabled)
4. Check the status/message displayed at the bottom 


**Expected Result:**

1. Chart Assistant should be online and responsive
2. It should process user queries and return AI-generated insights

**Actual Result:**

1. Chart Assistant shows "Offline" status
2. Error message: "Backend offline. Check http://127.0.0.1:8000"
3. No response from the assistant


**Bug -5** 
**Title**
Recent Insights section has UI/UX inconsistencies and readability issues

**Description**
The “Recent Insights” section in the sidebar contains multiple UI/UX issues affecting visual consistency, readability, and user interaction clarity.

**Observed problems include:**

1. Inconsistent timestamp formats (e.g., “2h ago”, “5h ago”, “Yesterday”)
2. Low contrast of timestamp text, reducing readability
3. Lack of clear visual hierarchy between section title and items
4. Insight items appear clickable but lack proper hover/interaction feedback
5. Insufficient spacing and separation between insight cards
6. Minor alignment and padding inconsistencies within cards
7. No active/selected state indication for selected insight
8. No handling for long lists (missing scroll or “View All” option)

These issues collectively impact usability and make the interface feel less polished.
**Expected Result**

1. Consistent timestamp format across all items
2. Improved text contrast for better readability
3. Clear visual hierarchy for section title
4. Proper hover and click feedback for interactive elements
5. Uniform spacing, alignment, and padding
6. Visible active/selected state for items
7. Scalable design with scroll or “View All” option

**Actual Result**

1. Mixed timestamp formats
2. Low visibility of secondary text
3. Weak visual distinction between elements
4. No interaction feedback
5. Minor alignment and spacing inconsistencies
6. No scalability for additional insights

**Steps to Reproduce**

1. Open the Dashboard page
2. Navigate to the left sidebar
3. Observe the “Recent Insights” section

**Impact**

1. Reduces readability and accessibility
2. Causes confusion about interactivity
3. Affects overall UI consistency and user experience 


**Bug -6** 
**Title**
Sidebar logo and header format changes inconsistently across navigation tabs

**Description**
When navigating between different sections in the application, the sidebar logo and header format are inconsistent.

1. On the Dashboard page, the sidebar displays the logo as “InsightEngine” with a specific layout and styling.
2. However, when navigating to Chart Explorer or Data Sources, the logo changes to “InsightEngine AI” and the formatting/layout appears different.

This inconsistency creates a visual mismatch and breaks UI uniformity across the application.


**Steps to Reproduce:**

1. Open the application
2. Click on Dashboard
3. Observe the sidebar logo and layout
4. Navigate to Chart Explorer
5. Navigate to Data Sources
6. Compare the sidebar logo and header formatting

**Actual Result:**

1. Sidebar logo text and design change between pages
2. Layout and formatting are inconsistent across sections

**Expected Result**

1. Sidebar logo and header should remain consistent across all pages
2. Branding (“InsightEngine”) and layout should not change when navigating

**Impact**

1. Breaks UI consistency and branding
2. Creates confusion for users
3. Reduces overall product quality perception


**Bug -7** 
**Title**
Incorrect table selection in backend query when question does not explicitly specify table name
 
 **Description**
 While testing the backend via Swagger, the system generates incorrect queries when a natural language question is asked without specifying the table name.

For example, when asking:
**“How many Yearly plan subscriptions were there in 2026 for all countries?”**

1. The API returns a 200 OK response, but
2. The generated query fetches data from multiple tables (e.g., vpn_test and vpn_test1), even though only vpn_test1 should be used.

However, when the same question is asked with the table name explicitly mentioned, the system returns the correct response using the intended table (vpn_test1).

**Steps to Reproduce**

1. Open Swagger UI
2. Use the query/ask endpoint
3. Enter the question:
4. “How many Yearly plan subscriptions were there in 2026 for all countries?”
5. Execute the request
6. Observe the generated query or response source

**Actual Result**

1. API returns 200 OK
2. Query pulls data from multiple tables (vpn_test, vpn_test1)
3. Result may be incorrect or inconsistent

**Expected Result**

1. Query should use only the intended table (vpn_test1)
2. System should correctly infer the relevant table without requiring explicit mention
3. Response should be accurate and consistent

**Impact**

1. Incorrect data retrieval
2. Reduces trust in analytics results
3. Requires users to manually specify table names (poor UX)

**Bug -8** 
**Title**
Backend API Testing and Validation in Swagger

**Description**
Performed backend API testing and validation using Swagger for the available services and endpoints. Verified API functionality by testing various request scenarios and validating response payloads against the expected results.

**The testing activities included:**

1.Validating request parameters, request bodies, and response structures.
2.Verifying HTTP status codes for successful, failed, and edge-case scenarios.
3.Testing authentication and authorization mechanisms.
4.Comparing API responses with database records to ensure data consistency and accuracy.
5.Identifying and documenting any mismatches, defects, validation issues, or unexpected 6.behaviors in the backend implementation.
6.Reporting findings and coordinating with the development team for issue resolution.

**Outcome:**
Ensured that backend APIs function as expected and highlighted discrepancies between the API responses and underlying database data for further investigation and fixes.



**Bug -9** 
**Title**
Dashboard Tabs and Sections Are Non-Clickable – Navigation/Redirection Not Working

**Description**
In the Analytics Dashboard, multiple tabs, cards, widgets, and sections are displayed but do not perform any action when clicked. Users are unable to navigate to the related detailed pages or modules from the dashboard.

Currently, sections such as:

1. Dashboard menu items
2. Revenue Performance widget
3. Recent Insights cards
4. AI Assistant action buttons
5. Summary cards (Total Revenue, Active Users, Avg Churn Rate)
6. Other visible tabs/sections

do not have clickable functionality or page redirection.

**Expected** Behavior:

1. Every interactive tab, card, widget, and section should be clickable.
2. On click, the user should be redirected to the corresponding detailed page/module/report.
3. Proper navigation routing should be implemented for all dashboard components.

**Actual Behavior:**

1. Clicking on tabs/sections/cards does nothing.
2. No navigation or action is triggered.
3. Dashboard appears static and non-interactive.

**Steps to Reproduce:**

1. Open Analytics Dashboard.
2. Click on any dashboard section/tab/card/widget.
3. Observe that no action or redirection occurs.


**Bug -10** 
**Title**
System Health and Security Review Cards Missing Hover Interaction on Data Sources Page

**Description:**
On the Data Sources page, the “System Health” and “Security Review” side cards are not responding to mouse hover interactions. When the cursor is moved over these sections, there is no hover effect, animation, highlight, elevation, or visual feedback.

These cards currently appear static, which creates an inconsistent user experience compared to other interactive UI components in the application.


**Affected Sections:**

1. System Health card
2. Security Review card

**Expected Behavior:**

1. Cards should respond visually on mouse hover.
2. Hover interaction may include:
      1. Slight movement/elevation
      2.Shadow effect
      3. Highlight/border effect
      4. Pointer cursor
      5. Smooth transition animation
3.UI behavior should be consistent with other interactive dashboard components.

**Actual Behavior:**

1. No hover effect or movement occurs when hovering over the cards.
2. Sections appear non-interactive/static.

**Steps to Reproduce:**

1. Open the Data Sources page.
2. Move the mouse cursor over:
     1. System Health card
     2. Security Review card
3.Observe that no hover interaction or visual feedback is displayed.