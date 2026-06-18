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


**Bug -11** 
**Title**
Swagger API Returns HTTP 200 Success but Generates Incorrect/Irrelevant AI Response

**Description:**
In the backend Swagger API (/api/query), the request is returning HTTP status code 200 OK, but the AI-generated response is not relevant to the user query.

When a user asks a specific analytical question, the API successfully executes without server error, but the returned content contains unrelated summaries, recommendations, or generic analytics text instead of the expected answer.

This appears to be an AI/model response handling issue rather than an API failure.

**Sample Query:**

{
  "query": "how many subscription plans are their in 2026 for brazil country?"
  "query":"How many subscription plans are there in Brazil in 2026?"
}

**Actual Response:**

1. API returns 200 OK
2. Response contains unrelated analytics summary/recommendation text
3. Does not provide the requested subscription count/details

**Expected Response:**

1. AI should generate an accurate response related to the asked query.
2. Returned data should match the requested analytics/question context.
3. Response should contain correct subscription plan information for Brazil in 2026.

**Observed Issue:**

1. Backend/API layer works successfully.
2. AI model response generation is producing incorrect or irrelevant output.
3. Possible causes:
     1. Incorrect prompt handling
     2. Model context issue
     3. SQL/query generation mismatch
     4. AI response parsing issue

**Steps to Reproduce:**

1. Open Swagger API documentation.
2. Execute POST /api/query.
3. Enter a valid analytics question in the request body.
4. Click Execute.
5. Observe that:
     1. Status code is 200
     2. Response content is unrelated to the actual query


**Bug -12** 
**Title**    
Latest Local Changes Not Reflecting on Server After Deployment

**Description**

The latest changes are working correctly in the local environment in forntend, but they are not reflecting on the server after deployment.

make sure to fix ASAP..

**Steps to Reproduce**

1. Make changes in the local environment
2. Verify the changes are working locally
3. Deploy the latest code to the server
4. Open the server application
5. Observe that the latest changes are not visible on the server

**Expected Result**
The server should reflect all the latest deployed changes.


**Actual Result**

The server is still showing old data/UI/functionality and not reflecting the latest updates.

**Bug -13** 
**Title**    
Resource Allocation Chart Layout and Tooltip Visibility Issues

**Description**

Multiple UI issues were identified in the Resource Allocation chart component affecting readability, alignment, and overall user experience.

**Issues Observed**

1. The chart tooltip overlaps the graph bars and blocks visibility of the chart data while hovering.
2. The Maintenance legend text has very low contrast and is difficult to read against the background.
3. The chart appears compressed within the card container due to improper spacing and alignment.
4. Y-axis labels are positioned too close to the chart border, affecting readability


**Steps to Reproduce**

1. Open the dashboard page
2. Navigate to the Resource Allocation chart section
3. Hover over the chart bars
4. Observe the tooltip behavior and chart layout

**Expected Result**

1. Tooltip should appear without blocking important chart data
2. Legend text should be clearly visible
3. Chart should have proper spacing and alignment within the container
4. Axis labels should have sufficient padding for better readability

**Actual Result**

1. Tooltip overlaps chart content
2. Legend text visibility is poor
3. Chart spacing/alignment appears uneven
4. Axis labels are too close to the border

**Bug -14** 
**Title**
Search Bar Text Visibility Issue and Refresh Charts Button Not Functioning Properly in Chart Explorer

**Description:**
In the Chart Explorer page, there are two issues identified in the highlighted section:

1. **Search Bar Text Visibility Issue:**

When entering text into the search bar, the typed text is not clearly visible due to poor text contrast/background styling. This makes it difficult for users to read the entered content.

2. **Refresh Charts Button Issue:**

When clicking the "Refresh Charts" button, the expected refresh action is not working properly. The charts are not updating/reloading as expected, and there is no proper response or feedback after clicking the button.


**Steps to Reproduce:**

1. Navigate to the Chart Explorer page.
2. Enter text into the search bar.
3. Observe the text visibility issue inside the input field.
4. Click on the Refresh Charts button.
5. Observe that the refresh functionality is not working correctly.

**Expected Result:**

1. Typed text in the search bar should be clearly visible.
2. Refresh Charts button should properly reload/update the charts.

**Actual Result:**

1. Search input text is unclear and difficult to read.
2. Refresh Charts button action is not functioning as expected.


**Bug -15** 
**Title**
Create Free Trial ClickHouse Database for VPN Analytics Project

**Description**

Set up a free trial ClickHouse database environment for the VPN Analytics project to support backend development, API testing, and analytics data storage.

**Requirements**

1. Create a free trial ClickHouse account
2. Configure a new database instance
3. Create database: vpn_test1
4. Verify database connectivity from backend application
5. Share connection details securely with the development team
6. Validate CRUD operations and query execution
7. Ensure environment variables/configuration are properly updated

**Acceptance Criteria**

1. ClickHouse free trial account is successfully created
2. vpn_test1 database is available and accessible
3. Backend is able to connect without errors
4. Test queries execute successfully
5. Connection credentials are documented securely..


**Bug -16** 
**Title**
Sidebar Navigation Alignment and Spacing Issue on Dashboard Page

**Description:**
On the Dashboard page, the left-side navigation panel inside the highlighted section has UI alignment and spacing inconsistencies. The sidebar menu items appear improperly spaced and visually unbalanced within the container.

The navigation section does not maintain proper padding and alignment consistency between menu items such as:

1. Dashboard
2. Chart Explorer
3. Data Sources
4. Mobile Admin

This affects the overall visual appearance and user experience of the sidebar navigation.

**Steps to Reproduce:**

1. Open the Dashboard page.
2. Observe the left-side navigation panel.
3. Check the spacing and alignment between sidebar menu items inside the highlighted section.

**Expected Result:**

1. Sidebar menu items should have consistent spacing, alignment, and padding.
2. Navigation section should appear visually balanced and properly structured.

**Actual Result:**

1. Sidebar items appear misaligned with inconsistent spacing and layout presentation.

Reason: The issue impacts UI consistency and user experience but does not block functionality.

**Bug -17** 
**Title**
Swagger Query API Returns OPENAI_API_KEY not set Message Instead of Actual Response

**Description:**
While testing the /api/query endpoint in Swagger UI, the API is returning an environment configuration error instead of processing the user query.

**Steps to Reproduce:**

1. Open Swagger UI.
2. Navigate to POST /api/query.
3. Enter a valid query in the request body.

**Example:**

{
  "query": "How many active users in express vpn in enterprise plan in Australia for February month in 2026?"
}

4.Click on Execute.


**Actual Result:**

API returns the following response:

{
  "content": "OPENAI_API_KEY not set. Please set the OPENAI_API_KEY environment variable."
}

**Expected Result:**

The API should process the query successfully and return the requested analytics/data response instead of an environment variable error.


**Impact:**

1. Swagger API testing is blocked.
2. Query endpoint is not functional due to missing backend environment configuration.
3. Users cannot validate query responses.

**Possible Cause:**

OPENAI_API_KEY environment variable is missing or not configured in the backend/server environment.


**Bug -18** 
**Title**
AI Assistant Chatbot Does Not Return Response After User Submits Query
 
**Description:**
When a user submits a question in the AI Assistant chatbot, the chatbot does not generate or display any response. After entering the query, the chat remains stuck in the “Analyzing historical dataset... Comparing growth vectors.” state without returning any result or error message to the user.

Additionally, the dashboard displays the error message:
Failed to load data: Request failed: 500

This indicates a possible backend/API failure affecting chatbot response generation.


**Steps to Reproduce:**

1. Open the Dashboard page
2. Launch the AI Assistant chatbot panel
3. Enter a query (e.g., “How many active users in express vpn in enterprise plan in Australia for February month in 2026?”)
4. Submit the question

**Actual Result:**

1. Chatbot does not provide any response
2. Loading/analyzing message continues indefinitely
3. Dashboard shows Request failed: 500 error

**Expected Result:**

1. Chatbot should process the query and return the requested analytics response successfully
2. Proper error handling should be shown if the request fails

**Possible Impact:**
Users are unable to retrieve insights or analytics data through the AI Assistant chatbot.

**Bug -19** 
**Title**
Connection Wizard Fields Remain Disabled and Database Selection State Is Not Visually Reflected in Data Sources page

**Description:**
In the Connection Wizard section, when a user selects a database type such as PostgreSQL, MongoDB, or BigQuery, the selected card does not display a clear active/selected state.

Additionally, the related configuration input fields (Host Address, Port, Database Name, etc.) remain visually disabled or inactive, creating confusion about whether the fields are editable.

This impacts user experience and makes the connection setup flow unclear.

**Steps to Reproduce**

1. Navigate to Data Sources page
2. Open Connection Wizard
3. Select any database type (PostgreSQL/MongoDB/BigQuery)
4. Observe the database card selection state
5. Check the input fields below


**Actual Result:**

1. Selected database card does not show a clear highlighted/active state
2. Input fields appear greyed out or disabled
3. Poor visual feedback for selected option
4. Users may assume fields are non-editable


**Expected Result:**

1. Selected database card should display a clear active/highlighted state
2. Related input fields should become visually enabled and editable
3. Proper UI feedback should guide the user through the setup process

**Bug -20** 
**Title**
Horizontal Scrollbar Visible in Active Data Sources Table Causing Poor UI Experience

**Description**

The “Active Data Sources” table displays a horizontal scrollbar within the table container even in desktop view where sufficient screen space is available.

The table layout is not properly responsive/aligned inside the container, causing unnecessary horizontal scrolling and reducing readability for users.

**Steps to Reproduce**

1. Navigate to Data Sources page
2. Scroll down to the “Active Data Sources” section
3. Observe the bottom area of the table container

**Actual Result**

1. Horizontal scrollbar appears inside the table
2. Table content overflows container width
3. Users must scroll horizontally to view complete data
4. Poor table responsiveness and UI alignment


**Expected Result**

1. Table should fit properly within the container width
2. Columns should align responsively without overflow
3. Horizontal scrollbar should not appear unnecessarily in desktop view
4. Users should view all important columns without manual scrolling


**Bug -21** 
**Title**
Revenue Performance Chart Container Displays Blank State After API Failure
 
 **Description**

The "Revenue Performance" chart section becomes completely blank when the API request fails with a 500 Internal Server Error. Although an error message is displayed at the top of the dashboard, the chart container itself does not provide any fallback UI, loading indicator, retry option, or meaningful empty/error state.

This creates a poor user experience because users cannot determine whether the chart is still loading, failed to load, or contains no data.

**Steps to Reproduce**

1. Open the Analytics Dashboard.
2. Navigate to the Dashboard Overview page.
3. Trigger or simulate a failed API response (500 Internal Server Error) for the revenue chart API.
4. Observe the Revenue Performance chart section.

**Expected Result**

The chart section should handle API failures gracefully by displaying one of the following:

1. Valid chart data (if API succeeds)
2. Loading state while fetching data
3. Meaningful error state/message inside the chart container
4. Empty-state UI when no data is available
5. Retry action/button for failed requests

**Actual Result**

The Revenue Performance chart area displays a large empty blank container after the API failure, with no fallback UI or recovery action available.

**Impact**

1. Poor user experience
2. Confusing blank dashboard state
3. No indication of chart failure inside component
4. Users may assume application is broken or still loading

**Bug -22** 
**Title**
Dashboard KPI Cards Display Placeholder Values Instead of Proper Error State During API Failure

**Description**
Dashboard KPI widgets including:

1. Total Revenue
2. Active Users
3. Avg Churn Rate

display placeholder dashes (—) when API requests fail. The widgets do not provide any meaningful error state, retry action, or unavailable-data message.

This makes the dashboard appear incomplete and does not clearly communicate that data loading has failed.

**Steps to Reproduce**

1. Open the Analytics Dashboard.
2. Navigate to the Dashboard Overview page.
3. Trigger or simulate a failed KPI metrics API response.
4. Observe the KPI cards section.

**Expected Result**

KPI widgets should:

1. display actual metric values when API succeeds,
2. show loading state while fetching data,
3. or display meaningful fallback/error state with retry option when API fails.

**Actual Result**

KPI cards display placeholder dashes (—) without any explanation or recovery option.


**Bug -23** 
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


**Bug -24** 
**Title**
User Signup API Returns 500 Internal Server Error Even with Valid Credentials

**Description:**
While testing the Signup API endpoint in Swagger, the API returns a 500 Internal Server Error even when valid user registration details are provided.

The request payload contains all required fields with correct values, but the user registration is not completed successfully. This indicates an issue on the backend/server-side handling of the signup process.

**Environment:**

1. API Endpoint: /auth/signup
2. Platform: Swagger API Docs
3. Environment: Production/UAT


**Steps to Reproduce:**

1. Open Swagger API documentation.
2. Navigate to POST /auth/signup.
3. Enter valid signup details:
  1.Email
  2.Phone number
  3.Password
  4.Confirm password
  5.Role
4.Click on Execute.
5.Observe the API response.


**Actual Result:**
API returns:

1. Status Code: 500 Internal Server Error
2. Response Message: Internal Server Error

**Expected Result:**
The API should successfully register the user and return:

1. Status Code: 200 OK or 201 Created
2. Success response with user/account creation confirmation.


**Bug -25** 
**Title**
Generating reports API Throws ClickHouse Type Error During Yearly Subscription Report Generation by Country

**Description**

When attempting to generate a CSV,PDF,PPT report for yearly plan subscriptions grouped by country for the year 2026 using the /files/generate API endpoint, the request fails with a ClickHouse database exception.

The backend appears to generate an invalid aggregation query where the SUM() function is applied to a String-type column, resulting in a database error and preventing CSV ,PDF,PPTreport generation.

This issue blocks users from exporting subscription analytics reports.

**Steps to Reproduce**

1. Open Swagger/API documentation
2. Navigate to:
         POST /files/generate
3.Enter the following prompt:
         Generate a csv report of yearly plan subscriptions by country in 2026
4.Click on Execute
5.Check the API response

**Actual Result**

1.API returns HTTP 500 error with the following database exception:
     {
  "message": "DB::Exception: Illegal type String of argument for aggregate function SUM. (ILLEGAL_TYPE_OF_ARGUMENT)"
}
2.CSV report is not generated
3.Download option fails
4.Backend query execution breaks

**Expected Result**

1. API should successfully process the request
2. CSV report should be generated and downloadable
3. Report should contain yearly subscription counts grouped by country for 2026
4. API should return successful response without database exceptions

**Bug -26** 
**Title**
Recent Insights Card Redirects to 404 Page Instead of Opening Insight Details

**Description:**
When clicking on the "Revenue Growth" card under the Recent Insights section in the left sidebar, the application redirects to a 404 – This page could not be found error page instead of opening the corresponding insight details or report page.

**Steps to Reproduce:**

1. Open the Insights dashboard.
2. Navigate to the Recent Insights section.
3. Click on the "Revenue Growth" insight card.

**Expected Result:**
The selected insight should open the corresponding insight/report details page successfully.

**Actual Result:**
Application redirects to a 404 page not found error screen.


**Bug -27** 
**Title**
Sidebar Collapse Expands Menu Text Outside Layout on Hamburger Icon Click

**Description:**
When the user clicks the hamburger (3-line) menu icon in the Mobile Store Admin sidebar, the sidebar partially collapses, but the navigation menu labels (Dashboard, Chart Explorer, Data Sources, Mobile Admin, etc.) overflow outside the sidebar container instead of resizing or hiding properly.

**Actual Result:**

1. Sidebar width reduces after clicking the hamburger icon
2. Menu text remains visible outside the collapsed sidebar
3. Navigation labels overlap the main content area
4. Sidebar layout appears broken and misaligned

**Expected Result:**

1. Sidebar should collapse cleanly within its container
2. Menu labels should either:
     1.hide completely, or
     2.appear properly aligned inside the collapsed sidebar
3.No text overflow or UI overlap should occur
4.Main content layout should remain properly aligned

**Steps to Reproduce:**

1. Open the Mobile Store Admin page
2. Click the hamburger (3-line) menu icon in the top-left sidebar
3. Observe the sidebar collapse behavior

**Issue Type:**
UI/UX Layout Bug

**Possible Cause:**
Sidebar collapsed state width is reduced, but menu label visibility/overflow styling is not handled correctly (overflow, display, width, or transition issue).


**Bug -28** 
**Title**
“View All Insights” Button Redirects to 404 Page Instead of Insights Listing

**Description:**
When the user clicks the “View All Insights” button in the left sidebar under the Recent Insights section, the application redirects to a 404 – This page could not be found error page instead of loading the expected Insights page.

**Actual Result:**

1. Clicking the “View All Insights” button opens a 404 error page
2. User is unable to access the complete Insights listing page

**Expected Result:**

1. Clicking the “View All Insights” button should navigate to the proper Insights dashboard/list page
2. All available insights should load successfully without any error

**Steps to Reproduce:**

1. Open the Insights Engine dashboard
2. Navigate to the left sidebar → Recent Insights section
3. Click on the “View All Insights” button
4. Observe the redirection behavior

**Issue Type:**
Functional / Navigation Bug

**Priority:**
High

**Impact:**
Users cannot access the complete insights section, which affects navigation flow and dashboard usability.

**Possible Cause:**

1. Incorrect route configuration
2. Missing frontend route/page
3. Backend endpoint or deployment issue
4. Broken navigation link path for /insights page

**Bug -29** 
**Title**
Mobile and Tablet Responsive Layout Is Broken – Dashboard Content, Sidebar, and Cards Are Not Properly Aligned
 
 **Description:**
The dashboard UI is not rendering correctly on mobile and tablet screen sizes. Multiple layout and responsiveness issues are visible when testing in responsive mode.

The sidebar occupies excessive space, causing the main dashboard content to become compressed and partially hidden. Insight cards, analytics sections, and text content are not adapting properly to smaller screens. Additionally, API failure messages and console errors are appearing, which further impacts the user experience.


**Steps to Reproduce:**

1. Open the application in Chrome browser
2. Navigate to the Analytics Dashboard page
3. Open Chrome DevTools (F12 or Ctrl + Shift + I)
4. Enable Responsive/Device Toolbar mode (Ctrl + Shift + M)
5. Select mobile or tablet resolutions such as:
            1.360 × 740
            2. 375 × 667
6.Refresh the page after switching to responsive mode
7.Observe the dashboard layout, sidebar behavior, and insight cards
8.Open the Console tab in DevTools
9.Notice the layout breaking issues and multiple API errors (404 and 500) appearing in the console

**Actual Result:**

1. Sidebar overlaps or consumes most of the screen width on mobile/tablet views
2. Dashboard content is partially hidden or compressed
3. Insight cards and analytics sections are misaligned
4. Text and components are not responsive for smaller resolutions
5. Console shows multiple API errors (404 and 500 responses)
6. Layout spacing and component scaling are inconsistent across devices


**Expected Result:**

1. Sidebar should collapse or resize properly on mobile and tablet screens
2. Dashboard content should be fully visible and responsive
3. Cards, charts, and insight sections should align correctly without overflow
4. Proper spacing and scaling should be maintained across all screen sizes
5. No broken API requests or console errors should appear during responsive testing


**Bug -30** 
**Title**
Market Growth Trends and Resource Allocation Graphs Missing Axis Labels and Measurement Indicators

**Description:**
Both the “Market Growth Trends” and “Resource Allocation” graphs are displayed without proper axis labels, value measurements, or scale indicators. Users are unable to clearly identify the data values, units, or graph interpretation.

**Affected Sections:**

1. Market Growth Trends graph
2. Resource Allocation graph

**Steps to Reproduce:**
1. Login to the InsightEngine Reports application.
2. Navigate to the Chart Explorer page.
3. Scroll down to the:
      1.Market Growth Trends graph
      2.Resource Allocation graph
4.Observe the chart sections carefully.
**Issue Observed:**

1. X-axis and Y-axis labels are missing.
2. Measurement scales/values are not displayed.
3. Graph units and data indicators are unclear.
4. Users cannot properly identify chart data or compare values visually.

**Expected Result:**
Graphs should display:
1. X-axis and Y-axis labels
2. Proper measurement scales/values
3. Data indicators or units
4. Clear graph identification for accurate analysis

**Actual Result:**
Graphs are rendered without:
1. Measurement values
2. Axis identification
3. Scale markers
4. Proper data readability

This makes the charts difficult to understand and reduces reporting usability.


**Bug -31** 
**Title**
Dashboard Page Missing Vertical Scrollbar Prevents Users from Viewing Full Content

**Description:**
The Dashboard Overview page does not display a vertical scrollbar, preventing users from scrolling up and down to access the complete dashboard content.

Even though multiple dashboard sections and widgets are available below the visible screen area, the page remains fixed and users cannot navigate to the hidden content.

**Steps to Reproduce:**

1. Open the Dashboard Overview page.
2. Observe the page layout after loading.
3. Try scrolling down using the mouse wheel or trackpad.
4. Notice that the page does not scroll vertically.

**Expected Result:**
A vertical scrollbar should be available when the dashboard content exceeds the screen height, allowing users to scroll up and down smoothly.

**Actual Result:**
No vertical scrollbar is displayed, and users are unable to access content outside the visible viewport.


**Bug -32** 
**Title**
Notification Icon Click Action Not Working on Mobile Store Admin Dashboard

**Description:**
When users click the notification icon in the top-right corner of the Mobile Store Admin dashboard, no notification panel, dropdown, popup, or response is displayed.

The notification icon appears clickable, but it does not perform any action, which may confuse users and affect usability.

**Steps to Reproduce:**

1. Open the Mobile Store Admin dashboard.
2. Navigate to the top-right corner of the page.
3. Click the notification (bell) icon.
4. Observe the system behavior.

**Expected Result:**
Clicking the notification icon should open a notification dropdown, alerts panel, or display recent notifications.

**Actual Result:**
No action occurs after clicking the notification icon.


**Bug -33** 
**Title**
Reports Portal Displays “No Available Server” Error and Fails to Load Dashboard

**Description:**
When accessing the reports portal (reports.dealwallet.com), the application fails to load and only displays the message “no available server” on a blank page. Users are unable to access the dashboard or any report data.

This issue indicates that the backend server or service handling the request is unavailable or not responding properly.

**Steps to Reproduce:**

1. Open the browser
2. Navigate to reports.dealwallet.com
3. Observe the page after loading

**Actual Result:**
A blank page is displayed with the error message:
 no available server


**Expected Result:**
The reports dashboard should load successfully without any server availability errors.

**Bug -34** 
**Title**
Action Label Missing in Active Data Sources Table – Only Three-Dot Menu Displayed

**Description:**
In the Active Data Sources table, the Action column label is missing from the table header. Currently, only the three-dot action menu is displayed for each row without a visible “Action” or “Options” label. This causes unclear UI behavior and reduces usability because users may not understand the purpose of the menu icon.

**Steps to Reproduce:**

1. Login to the application
2. Navigate to the Active Data Sources page
3. Observe the table headers and row actions
4. Check the right-side column beside the Status column

**Actual Result:**
Only the three-dot menu icon is displayed beside the Status column, and the Action column label/header is missing.

**Expected Result:**
An Action (or appropriate label) column header should be displayed above the three-dot menu icons for better clarity and consistency.


**Bug -35** 
**Title**
Revenue Growth Percentage Displayed Even When Revenue Data Is Unavailable

**Description**

When the dashboard has no revenue data available, the Revenue Performance widget correctly displays “No data available” and the Total Revenue value is shown as empty (—). However, the growth percentage indicator still displays +12.5%.

The percentage value should not be displayed when there is no revenue data available because it creates misleading analytics information and inconsistent UI behavior.

**Steps to Reproduce**

1. Open the Analytics Dashboard
2. Load an account/environment with no revenue data
3. Observe the Revenue Performance section
4. Check the Total Revenue card on the right side

**Actual Result**

1. Revenue chart displays “No data available”
2. Total Revenue value displays —
3. Growth percentage still displays +12.5%

**Expected Result**
When no revenue data exists:
1. Growth percentage should be hidden, disabled, or shown as 0%
2. Dashboard metrics should remain consistent with the available data


**Bug -36** 
**Title**
AI Assistant Cannot Reach Backend & Dashboard Fails Due to Missing DB_HOST Environment Variable

**Description**

The analytics dashboard is showing a configuration error indicating that DB_HOST is not set in the environment configuration. Additionally, the AI Assistant panel cannot connect to the backend API running on 127.0.0.1:8000.

Because of this:

1. Dashboard widgets show no data
2. Revenue/User Growth sections are empty
3. AI Assistant queries fail
4. Backend connectivity is broken

**Steps to Reproduce**

1. Open Analytics Dashboard
2. Navigate to Dashboard page
3. Observe warning banner:
4. DB_HOST is not set. Check your .env file
5. Open AI Assistant
6. Ask any query
7. Observe backend connection error

**Actual Result**

1. Dashboard data not loading
2. AI Assistant unable to fetch responses
3. Backend connection failure shown

**Expected Result**

1. Dashboard should load analytics data successfully
2. AI Assistant should communicate with backend API
3. No environment variable errors should appear
**Possible Root Cause**

1. Missing or improperly loaded .env configuration
2. Backend server not running on port 8000
3. Database connection initialization failure

**Bug -37** 
**Title**
Global Performance Map UI Alignment Issue Inside Card Container

**Description**

The “Global Performance Map” visualization is not properly aligned within the dashboard card container. The map content appears too close to the card edges, especially near the bottom corners, causing inconsistent spacing and an unpolished UI appearance.

**Steps to Reproduce**

1. Open Chart Explorer page
2. Navigate to “Global Performance Map” widget
3. Observe the map alignment inside the container

**Actual Result**

1. Map visualization appears cramped near card edges
2. Bottom corners look misaligned
3. Inconsistent inner padding/margins
4. Content fitting inside the card looks improper

**Expected Result**

1. Map should have proper spacing from all card edges
2. Consistent padding should be maintained
3. Visualization should fit cleanly within rounded container borders

**Possible Root Cause**

1. Incorrect padding/margin values
2. Overflow handling issue
3. Improper canvas/image scaling inside container


**Bug -38** 
**Title**
Chart Explorer Displays “Failed to Fetch” Error While Loading Dashboard Data

**Description**

The Chart Explorer page fails to load analytics data and displays a Failed to fetch error banner. The frontend is unable to retrieve data from the backend API, causing dashboard visualizations and charts to become partially or fully non-functional.

**Steps to Reproduce**

1. Open the Analytics Dashboard
2. Navigate to the Chart Explorer page
3. Wait for dashboard data to load
4. Observe the error banner at the top

**Actual Result**

1. Failed to fetch error is displayed
2. Some dashboard components fail to load data
3. Analytics visualizations become unreliable/incomplete

**Expected Result**

1. Dashboard should successfully fetch data from backend APIs
2. Charts and analytics widgets should load without errors
3. No fetch failure message should appear

**Possible Root Cause**

1. Backend API unavailable
2. API endpoint failure
3. Network/CORS configuration issue
4. Incorrect API base URL
5. Timeout or internal server error


**Bug -39** 
**Title**
Dashboard displays raw environment configuration error message to end users

**Description:**
On the Dashboard Overview page, the application is displaying the technical error message:
DB_HOST is not set. Check your .env file.

This exposes internal backend/environment configuration details directly in the UI instead of showing a user-friendly error message. The issue appears in a visible alert banner on the dashboard and may confuse users while also exposing sensitive system configuration information.

**Steps to Reproduce:**

1. Login to the application
2. Navigate to the Dashboard Overview page
3. Observe the alert banner displayed below the page heading

**Actual Result:**
System displays the raw backend/environment error message:
DB_HOST is not set. Check your .env file.

**Expected Result:**
Application should handle configuration/database errors gracefully and display a generic user-friendly message such as:
Unable to load dashboard data. Please try again later.

**Impact:**

1. Exposes internal system configuration details
2. Poor user experience
3. Dashboard metrics and charts are not loading properly


**Bug -40** 
**Title**
Dashboard empty state text alignment is inconsistent in analytics widgets

**Description:**
The empty state messages (No data and No plan data) inside dashboard widgets are not properly aligned within their respective containers. The text positioning appears inconsistent and affects the visual layout of the dashboard.

**Steps to Reproduce:**

1. Login to the application
2. Navigate to the Dashboard Overview page
3. Observe the User Growth widget and Top Plans by Revenue widget
4. Check the placement of the empty state messages (No data and No plan data)
5. Notice that the text is not properly centered/aligned within the cards

**Actual Result:**
Empty state text is unevenly positioned and not properly centered within the cards.

**Expected Result:**
Empty state messages should be consistently centered and aligned within all dashboard widgets for better UI consistency.


**Bug -41** 
**Title**
Chart axis labels and starting month are not properly visible in Market Growth Trends graph
 
 **Description:**
In the “Market Growth Trends” chart, the X-axis and Y-axis indicators/labels are either missing or not clearly visible. Additionally, the line graph appears to start before the first visible month label, causing improper chart alignment and reducing readability.

The graph line starts from the left side, but the starting month label is not displayed correctly, creating confusion in data interpretation.

**Steps to Reproduce:**

1. Login to the application
2. Navigate to the Chart Explorer page
3. Scroll to the Market Growth Trends section
4. Observe the X-axis, Y-axis, and starting point of the graph

**Actual Result:**

1. X-axis labels are partially missing/inconsistent
2. Y-axis indicators are not clearly visible
3. Graph line starts before the first visible month label
4. Initial month alignment is incorrect

**Expected Result:**

1. Both X-axis and Y-axis labels should be clearly visible
2. The graph should properly align with the starting month
3. The first data point should begin exactly from the first visible month indicator


**Bug -42** 
**Title**
Date Range Filter Dropdown Options Not Displaying in Dashboard Overview

**Description:**
The date range filter in the Dashboard Overview page is currently displaying only the default option “Last 30 Days” without any dropdown functionality or additional selectable ranges.

Expected dropdown options such as:

1. Last 7 Days
2. Last 30 Days
3. Last 3 Months
4. Last 6 Months
5. Last 12 Months
6. Custom Range

are not visible when clicking the filter.

This prevents users from filtering dashboard analytics data based on different time periods.

**Steps to Reproduce:**

1. Login to the InsightEngine dashboard.
2. Navigate to the Dashboard Overview page.
3. Click on the “Last 30 Days” date filter dropdown at the top-right corner.
4. Observe that no dropdown options are displayed.

**Expected Result:**
The date filter should open a dropdown menu showing multiple selectable date ranges including “Last 12 Months” and other period options.

**Actual Result:**
Only “Last 30 Days” is displayed and no dropdown menu/options appear.


**Bug -43** 
**Title**
Recent Insights Tabs Are Displayed Too Close Together Without Proper Spacing

**Description:**
In the left sidebar under the Recent Insights section, the insight tabs/cards (Revenue Growth, User Demographics, and Churn Rate Analysis) are appearing too close to each other without proper spacing or padding. This makes the section look visually cluttered and reduces UI readability.

Proper spacing/margin should be maintained between each insight card to improve alignment, readability, and overall user experience.

**Steps to Reproduce:**

1. Open the Chart Explorer page.
2. Navigate to the left sidebar.
3. Observe the Recent Insights section.
4. Check the spacing between the insight cards.

**Expected Result:**
Each insight card should have consistent spacing and padding between items.

**Actual Result:**
The insight cards are displayed in a mixed/cluttered manner with little or no spacing between them.


**Bug -44** 
**Title**
Incorrect Period Label Displayed as "12 Mo" Instead of "12 Months" in Dropdown
 
 **Description:**
In the Market Growth Trends section, the period filter dropdown is displaying abbreviated values such as "12 Mo", "6 Mo", and "3 Mo". As per the expected UI/content format, the period labels should be displayed in full text such as "12 Months", "6 Months", and "3 Months" for better clarity and readability.

**Steps to Reproduce:**

1. Open the dashboard page.
2. Navigate to the Market Growth Trends widget.
3. Click on the period dropdown.
4. Observe the displayed dropdown values.

**Expected Result:**
Dropdown values should display as:
1. 12 Months
2. 6 Months
3. 3 Months

**Actual Result:**
Dropdown values are displayed in abbreviated format:
1. 12 Mo
2. 6 Mo
3. 3 Mo


**Bug -45** 
**Title**
Search Query Is Not Cleared After Clicking Refresh in Chart Explorer

**Description**

In the Chart Explorer page, when a user searches for any report using the search bar and then clicks the Refresh button, the page data refreshes successfully, but the previously entered search text remains in the search field instead of being cleared.

The expected behavior is that the search input should reset/clear after clicking the Refresh button so that the page returns to its default state.

**Steps to Reproduce**

1. Open the Chart Explorer page.
2. Enter any text in the search bar (example: brazil reports).
3. Click the Refresh button.
4. Observe the search field after refresh.

**Actual Result**

The page refreshes, but the previously entered search text remains visible in the search bar.

**Expected Result**

After clicking the Refresh button, the search field should be cleared and reset to the default state