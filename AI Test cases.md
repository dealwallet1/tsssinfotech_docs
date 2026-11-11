**BUG : 1**
Title:QA Testing – E-Commerce Assistant Multi-Agent  AI-Chatbot Exploring on Project Doc

**Description:**
Perform comprehensive QA testing of the E-Commerce Assistant application based on the Technical User Guide.

The application contains four specialised AI agents: Store Manager, Finance, Legal and Technical. Testing must verify agent selection, query routing, response accuracy, document retrieval, source citations, calculations, conversation context and error handling.

The objective is to validate that each agent processes user queries correctly and provides accurate, relevant and traceable responses.

**Scope of Testing**
1. Agent Selection and Routing
Verify all four agents are available in the category selector.

Verify the selected agent name and specialisation are displayed correctly.

Verify queries are routed to the appropriate agent.

Verify responses from one agent are not incorrectly returned by another agent.

Test switching between agents during a conversation.

2. Store Manager Agent
Validate order and revenue information.

Verify monthly and month-over-month revenue comparisons.

Validate customer and product performance analysis.

Verify highest-order days and sales trends.

Test chained queries and multiple lookups.

Validate missing, incorrect and unavailable store data.

3. Finance Agent
Validate GST and TCS-related responses.

Verify marketplace commission calculations.

Test UPI and payment gateway fee calculations.

Validate seller settlement and payout calculations.

Test refund deductions and fee reversals.

Verify calculation accuracy with different amounts, rates and missing inputs.

4. Legal Agent
Validate consumer protection and e-commerce compliance responses.

Test return, replacement and refund policy queries.

Verify original price and discount-related responses.

Test dark patterns and misleading advertisements.

Validate incentivised review and rating-related responses.

Verify source-grounded legal answers and citations.

5. Technical Agent
Validate API and webhook-related answers.

Test webhook signature verification queries.

Verify duplicate order and payment prevention guidance.

Test inventory synchronization scenarios.

Validate rate-limit and payment error-code responses.

Test retry mechanisms and delayed webhook scenarios.

6. RAG and Source Citation Validation
Verify relevant knowledge-base documents are retrieved.

Verify references are displayed at the end of applicable answers.

Verify clicking a reference opens the correct source preview.

Validate source file names, original content and document preview.

Test queries where no relevant document is available.

Verify unsupported answers are not presented as confirmed facts.

7. Conversation and Follow-up Testing
Verify follow-up questions retain previous conversation context.

Test multiple consecutive questions.

Verify context is not incorrectly mixed between unrelated topics.

Test switching agents and continuing conversations.

**Testing Types**
Positive Testing

Negative Testing

Boundary Value Testing

Edge Case Testing

Functional Testing

Integration Testing

Response Accuracy Testing

Calculation Validation

RAG and Citation Testing

Regression Testing

UI Testing

**Expected Result**
All four agents should handle their respective domain queries correctly.

Queries should be routed to the appropriate specialist.

Responses should be relevant, accurate and supported by the appropriate evidence.

Financial calculations should produce mathematically correct results.

Document references should open the correct source.

Follow-up questions should retain relevant context.

Invalid, incomplete and unsupported queries should be handled gracefully.

No application crashes, unexpected errors or incorrect agent responses should occur.

**Acceptance Criteria**
All four agents are accessible and selectable.

Agent routing works correctly.

Positive and negative scenarios are executed.

Boundary and edge cases are validated.

Financial calculations are verified independently.

RAG retrieval and source citations are validated.

Follow-up conversation context is verified.

All identified defects are documented as separate GitHub issues.

Test execution results and evidence are documented.

Regression testing is completed after defect fixes.

**Issue Type: QA / Testing**

**Priority: High**

**Labels: QA, Testing, E-Commerce-Assistant, Functional-Testing, Regression-Testing**

**QA Deliverables**
Detailed test cases for all four agents.

Positive, negative and edge-case test scenarios.

**Test execution results.**

Screenshots and evidence for failed scenarios.

Individual GitHub bug reports.

Final QA testing summary.

**BUG : 2**
Title:E-Commerce Assistant Requirement Analysis and Test Case Preparation

**Description**
Completed the exploration and analysis of the E-Commerce Assistant Technical User Guide

Reviewed the project requirements, functionalities and workflows of all four specialised AI agents to understand the expected application behaviour before starting functional testing.

Based on the requirement document, prepared detailed test cases covering positive, negative and edge-case scenarios for each agent.

**Activities Completed**
1. Requirement Document Exploration
Reviewed the E-Commerce Assistant Technical User Guide.

Understood the overall multi-agent chatbot architecture and workflow.

Explored the four specialised agents and their responsibilities.

Understood agent selection and query routing.

Reviewed RAG-based responses and knowledge-base document retrieval.

Explored source citations and document preview functionality.

Reviewed follow-up queries and conversation context.

Understood tool-based calculations and data retrieval workflows.

2. Agent-Wise Requirement Analysis
Store Manager Agent

Orders, revenue and sales analytics.

Customer and product performance.

Monthly revenue comparisons.

Cancellation and peak-day analysis.

Finance Agent

GST and TCS calculations.

Marketplace commissions and payment charges.

UPI fees and seller settlements.

Refund deductions and payout reconciliation.

Legal Agent

Consumer protection regulations.

Return, replacement and refund policies.

Pricing claims and dark patterns.

Reviews, ratings and customer consent.

Technical Agent

API and webhook integrations.

Signature verification.

Duplicate order and payment prevention.

Inventory synchronization.

Rate limits and payment error handling.

3. Test Case Preparation
Prepared an Excel workbook containing 87 test cases covering:

Positive test scenarios.

Negative test scenarios.

Edge-case scenarios.

Agent selection and routing validation.

Response accuracy validation.

RAG and source citation validation.

Follow-up conversation context validation.

Financial calculation validation.

The test cases include test case IDs, scenarios, preconditions, execution steps, sample chatbot queries, expected results and priority levels.

**Acceptance Criteria**
Requirement document exploration completed.

All four agent functionalities reviewed

Application workflows and query routing understood.

RAG and source citation requirements reviewed.

Positive test cases prepared.

Negative test cases prepared.

Edge-case scenarios prepared.

Excel test case workbook created.

Begin functional test execution.

Validate chatbot responses against requirements.

Document defects and create individual GitHub bug tickets.

**Issue Type: QA Task**

**Priority: High**

**Labels: QA, Test-Cases, Requirement-Analysis, E-Commerce-Assistant**

**Next Steps**
Start functional testing of all four agents using the prepared test cases, validate actual responses against expected results, capture evidence for failures and report identified defects through separate GitHub issues.

**BUG : 3**
Title:API Key Required Popup Displays 403 Error When Opening LightRAG Application Without an API Key

**Description**
When a user opens the LightRAG application, an API Key Required popup is displayed asking the user to enter an API key to access the service.

Displaying this popup is expected behavior because API authentication is required. However, when the user opens the application without entering an API key, the application displays a raw 403 error message below the API key input field:

403 {"detail":"API Key required"}/graphs?label=*&max_depth=3&max_nodes=1000

The application should handle this authentication scenario gracefully instead of exposing a raw API error message to the user.

**Preconditions**
LightRAG application is accessible.

User does not have an API key entered or saved.

User opens the application in a browser.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to the Chatbot section.

Observe the API Key Required popup.

Do not enter any API key in the input field.

Observe the error message displayed below the API key input field.

Verify the HTTP 403 error response.

**Actual Result**
API Key Required popup appears when opening the application.

Without entering an API key, the application displays a raw 403 error message.

The error exposes backend API details, including the /graphs endpoint and request parameters.

The user cannot access the chatbot without providing a valid API key.

**Expected Result**
API Key Required popup should appear when no API key is configured.

The application should not display raw HTTP 403 responses or backend endpoint details.

The user should see a clear and user-friendly message, such as: "Please enter a valid API key to access the service."

The application should handle missing API key authentication gracefully without exposing backend implementation details.

After entering and saving a valid API key, the user should be able to access the chatbot successfully.

**Acceptance Criteria**
API Key Required popup appears when no API key is available.

No raw 403 error or backend endpoint details are displayed.

A user-friendly validation message is displayed when authentication is missing.

Empty API key submission is handled properly.

Invalid API keys display an appropriate authentication error.

Valid API keys allow successful chatbot access.

No unnecessary authentication errors appear in the UI.

**Impact: Poor user experience and exposure of raw backend error details during application initialization.**

**Priority: Medium**

**Issue Type: Bug**

**Priority: Medium**

**Module: LightRAG – Chatbot / API Authentication**

**BUG : 4**
Title:Login Free Button Is Non-Functional in LightRAG Application Header

**Description**
The LightRAG application header displays a Login Free button. However, clicking the button does not trigger any action or navigation.

The button appears to be interactive, but it does not provide any response when clicked. Additionally, the button label Login Free should be verified against the intended UI design.

**Preconditions**
LightRAG application is accessible.

User opens the application without logging in.

Chatbot page is loaded successfully.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to the Chatbot page.

Locate the Login Free button in the top navigation bar.

Click the Login Free button.

Observe whether any login popup, authentication page, or navigation action occurs.

**Actual Result**
Login Free button is displayed in the application header.

Clicking the button does not trigger any action.

No login popup or authentication page is displayed.

The button appears interactive but does not respond.

**Expected Result**
Clicking the Login button should trigger the intended login or authentication flow.

The application should navigate to the login page or display the appropriate login popup.

The button label should be consistent with the intended UI design.

**Acceptance Criteria**
Login button should perform its intended action.

Clicking the button should open the appropriate authentication interface.

The button should not appear interactive without providing functionality.

Button text should match the approved UI design.

Login functionality should work correctly without affecting existing chatbot functionality.

**Impact: Users may be confused because the application displays a login option that does not work.**

**Priority: Medium**

**Issue Type: Bug**

**Priority: Medium**

**Module: LightRAG – Header / Authentication**

**Environment: QA**

**BUG : 5**
**Title :**Improve Pipeline Status Popup with Completed, Pending, Processing, and Failed Document Counts

**Description**
The current Pipeline Status popup does not provide sufficient information about document-processing progress.

Currently, the popup displays:

Pipeline Busy indicator

Job Name

Start Time

Progress (0/0 Batch)

Pipeline Messages

However, it does not clearly display the number of completed, pending, processing, and failed documents.

To improve pipeline monitoring and provide better visibility, the Pipeline Status popup should display separate document counts for each processing status, along with the total document count and overall progress.

**Preconditions**
LightRAG application is accessible.

User navigates to the Document Management section.

Documents are uploaded into the application.

Pipeline processing is available.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to the Documents section.

Upload multiple documents.

Click the Pipeline button.

Observe the Pipeline Status popup.

Check whether completed, pending, processing, and failed document counts are displayed.

Verify whether the progress reflects the actual document-processing status.

**Actual Result**
Pipeline Status popup displays limited information.

Job Name and Start Time may display -.

Progress may display 0/0 Batch.

No separate document counts are available inside the popup for Completed, Pending, Processing, and Failed statuses.

Users cannot easily identify the overall document-processing status.

**Expected Result**
The Pipeline Status popup should display the following information:

Completed: Number of successfully processed documents.

Pending: Number of documents waiting for processing.

Processing: Number of documents currently being processed.

Failed: Number of documents that failed during processing.

Total: Total number of documents included in the pipeline.

**Proposed UI Improvements**
Display Completed count with a green indicator.

Display Pending count with a yellow indicator.

Display Processing count with a blue indicator.

Display Failed count with a red indicator.

Display Total document count.

Add a progress bar showing overall completion percentage.

Display Job Name, Start Time, and Elapsed Time.

Show meaningful pipeline messages and processing logs.

Update all counts and progress dynamically as document statuses change.

**Acceptance Criteria**
All four document statuses must be displayed separately.

Total document count must match the documents included in the pipeline.

Completed count must increase when documents finish successfully.

Pending count must decrease when documents enter processing.

Processing count must reflect currently running document jobs.

Failed count must increase when document processing fails.

Progress percentage must be calculated correctly.

All counts must update automatically or through the refresh action.

When no pipeline job is running, display a clear idle state.

Pipeline messages must provide meaningful information instead of displaying only -.

**Issue Type: Enhancement / UI Improvement**

**Module: LightRAG – Document Management / Pipeline**

**Priority: Medium**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**Impact**
Improves pipeline visibility, helps users monitor document-processing activities, makes failures easier to identify, and provides a clear overview of document-processing progress.


**BUG : 6**
**Title :**Chatbot Generates Responses When No Documents Are Uploaded

**Description**
When no PDF or other documents are uploaded into the Document Management section, the chatbot still generates responses to user queries with detailed product and sales information.

During testing, the Documents page displayed zero uploaded documents across all processing statuses. However, when a user submitted a product-related question through the Store Manager Chatbot, the chatbot returned product information, including SKU, product name, category, unit price, total units sold, total revenue, and order count.

This behavior needs to be verified against the expected knowledge source and chatbot configuration.

**Preconditions**
Open the LightRAG application.

Navigate to the Documents section.

Ensure no documents have been uploaded.

Verify that all document status counts are zero.

Navigate to the Chatbot section.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to Document Management.

Verify that the document list is empty.

Confirm that All, Completed, Parsing, Analyzing, Processing, and Failed counts are zero.

Navigate to the Chatbot section.

Select Store Manager Agent.

Enter the following question:

**"How many products do we have in the range of 3000?"**

Click Send.

Observe the chatbot response.

**Actual Result**
No documents are uploaded in the Document Management section.

The chatbot still generates a detailed response.

It returns product details, SKU numbers, unit prices, total units sold, revenue, and order counts.

The response does not indicate which knowledge source was used.

**Expected Result**
If the chatbot is configured to use uploaded documents as its only knowledge source:

It should not generate unsupported document-based answers when no documents are available.

It should display a meaningful message such as:

"No documents are currently available in the knowledge base. Please upload relevant documents before asking document-based questions."

It should not fabricate product or sales information.

It should clearly identify the source of information used to generate responses.

If the chatbot is designed to retrieve information from an independent business database, its responses should be validated against that database instead.

**Acceptance Criteria**
Chatbot should correctly identify whether relevant knowledge sources are available.

Document-based queries should not return unsupported answers when the document repository is empty.

Database-backed queries should work only when the appropriate database or tools are configured.

Responses should be grounded in the actual configured data source.

Chatbot should provide a clear message when the required knowledge source is unavailable.

The application should not generate fabricated information.

**Issue Type: Functional Bug**

**Priority: High (if document-based RAG is required)**

**Module: LightRAG – Chatbot / Document Management**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**Impact**
Users may receive misleading information because the chatbot generates detailed responses without clearly identifying the underlying data source.

**Priority: High if document-only RAG behavior is required.**

**BUG : 7**
**Title :**E-Commerce Chatbot Responds to General Knowledge Questions Outside Its Intended Domain

**Description**
The Store Manager Agent is designed to handle e-commerce-related queries, including store operations, orders, products, sales, revenue, and business performance.

However, during testing, the chatbot generates responses to general knowledge questions that are unrelated to e-commerce.

For example:

When asked "What is Python?", the chatbot provides a detailed explanation of the Python programming language.

When asked "Capital of Hyderabad?", the chatbot generates a general knowledge response about Hyderabad.

The chatbot should validate incoming queries against its intended business domain and prevent unrelated general knowledge responses.

**Preconditions**
LightRAG application is accessible.

Navigate to the Chatbot section.

Select the Store Manager Agent.

Ensure the chatbot is connected.

**Steps to Reproduce**
**Test Case 1: General Programming Question**

Open the LightRAG application.

Navigate to the Chatbot section.

Select Store Manager Agent.

Enter the question: "What is Python?"

Click Send.

Observe the chatbot response.

**Test Case 2: General Knowledge Question**

Enter the question: "Capital of Hyderabad?"

Click Send.

Observe the chatbot response.

**Actual Result**
Chatbot responds to general knowledge questions.

Provides detailed explanations unrelated to e-commerce.

Does not validate whether the question belongs to the Store Manager Agent's domain.

Does not display any out-of-scope warning or restriction message.

**Expected Result**
Chatbot should identify questions outside its supported e-commerce domain.

It should not provide general-purpose answers unrelated to its assigned responsibilities.

It should display a user-friendly message, such as:

**"I'm the Store Manager Assistant. I can help you with products, orders, sales, revenue, inventory, and store operations. Please ask an e-commerce-related question."**

**Acceptance Criteria**
Chatbot should answer relevant e-commerce and store-management questions.

General knowledge questions should be identified as out-of-scope.

Programming, geography, entertainment, and unrelated general knowledge questions should not receive general-purpose answers.

Appropriate out-of-scope messages should be displayed.

Relevant business queries should continue working correctly.

Domain validation should work consistently across chatbot sessions.

**Impact**
The chatbot may behave like a general-purpose AI assistant instead of a specialized E-Commerce Store Manager Agent. This reduces domain accuracy and affects the reliability of the application.

**Priority: High**

**Issue Type: Functional Bug**

**Module: LightRAG – Chatbot / Store Manager Agent**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**Reference: Attached screenshots showing responses to "What is Python?" and "Capital of Hyderabad?"**

**BUG : 8**
**Title :**Add Logout Confirmation Popup Before Ending User Session

**Description**
Currently, when a user clicks the Logout icon in the LightRAG application header, the application immediately logs out without displaying any confirmation message.

There is no confirmation popup to verify whether the user actually intends to log out.

To prevent accidental logout and improve user experience, a confirmation dialog should be displayed before terminating the current session.

**Preconditions**
User is logged into the LightRAG application.

User is accessing the Document Management or Chatbot section.

Logout icon is visible in the application header.

**Steps to Reproduce**
Open the LightRAG application.

Log in with valid credentials.

Navigate to the Document Management page.

Locate the Logout icon in the top-right corner.

Click the Logout icon.

Observe the application behavior.

**Actual Result**
Clicking the Logout icon immediately logs out the user.

No confirmation popup is displayed.

The user is redirected or logged out without an opportunity to cancel the action.

**Expected Result**
When the user clicks the Logout icon, the application should display a confirmation popup.

Suggested Confirmation Message:

**"Are you sure you want to log out?"**

The popup should provide two options:

**Yes, Logout: Terminates the current session and redirects the user to the appropriate login page.**

**No, Cancel: Closes the confirmation popup and keeps the user logged in on the current page.**

**Acceptance Criteria**
Clicking the Logout icon should display a confirmation popup.

The popup should clearly ask the user to confirm the logout action.

Clicking Yes should successfully terminate the current session.

Clicking No or Cancel should close the popup without logging out.

Clicking outside the popup or pressing Escape should not accidentally log out the user.

The confirmation dialog should work consistently on both Document Management and Chatbot pages.

Session data should be cleared only after the user confirms logout.

**Impact**
Users may accidentally lose their active session by clicking the Logout icon unintentionally. Adding a confirmation dialog prevents accidental logout and improves application usability.

**Priority: Medium**

**Issue Type: Enhancement / UI Improvement**

**Module: LightRAG – Authentication / User Session Management**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**BUG : 9**
**Title :**Incorrect Default Category Assigned to Uploaded Documents When No Category Is Selected

**Description**
When uploading a document through the Document Management section, the application allows users to submit the document without selecting a category from the category dropdown.

During testing, a Store Manager knowledge document (01_store_manager_knowledge.txt) was uploaded without selecting any category.

The upload was successful, but after submission, the application automatically assigned the category Legal to the uploaded document.

Since the uploaded document contains Store Manager-related information, assigning the Legal category is incorrect.

The application should handle missing category selections appropriately and should not assign an unrelated default category.

**Preconditions**
LightRAG application is accessible.

User is logged into the application.

Navigate to the Document Management section.

Ensure the document is not already uploaded.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to the Documents section.

Click the Upload button.

Select the file 01_store_manager_knowledge.txt.

Do not select any category from the Select Category dropdown.

Click Upload.

Wait for the upload to complete successfully.

Check the uploaded document in the Document Management table.

Observe the assigned category.

**Actual Result**
The document uploads successfully without selecting a category.

The application automatically assigns the Legal category.

The assigned category does not match the document's Store Manager-related content.

No warning or validation message is displayed when the category is left unselected.

**Expected Result**
The application should not automatically assign an unrelated category when no category is selected.

If category selection is mandatory, the application should display a validation message such as:

"Please select a document category before uploading."

If automatic categorization is supported, the application should identify the appropriate category based on the document content.

Store Manager knowledge documents should be assigned the appropriate Store Manager category.

The selected or automatically assigned category should be displayed correctly in the Document Management table.

**Acceptance Criteria**
Category selection should be validated before document submission if it is mandatory.

Documents should not receive an incorrect default category.

Store Manager documents should be assigned the appropriate category.

Finance documents should be assigned the Finance category.

Legal documents should be assigned the Legal category.

The assigned category should remain consistent after successful upload and processing.

A meaningful validation message should appear when a mandatory category is missing.

**Impact**
Incorrect category assignment can cause documents to be grouped under the wrong category, resulting in confusion during document management and potentially affecting category-based retrieval.

**Issue Type: Functional Bug**

**Priority: High**

**Module: LightRAG – Document Management / Document Upload**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**Evidence: Attached screenshots showing the upload process without category selection and the uploaded Store Manager document displayed under the Legal category.**

**BUG : 10**
**Title :**Add Recent Chat History, New Chat, and End Chat Options to Chatbot

**Description**
Currently, the LightRAG Chatbot interface does not display dedicated options to manage conversation sessions.

Users can submit multiple questions and receive responses in the same conversation, but there are no visible options to access recent chat history, start a new conversation, or end the current chat session.

To improve chatbot usability and conversation management, the application should provide these three functionalities.

**Preconditions**
LightRAG application is accessible.

User is logged into the application.

Navigate to the Chatbot section.

Select the Store Manager Agent.

Submit at least one question to create a conversation.

**Steps to Reproduce**
Open the LightRAG application.

Navigate to the Chatbot section.

Select Store Manager Agent.

Submit multiple questions.

Observe the chatbot header and conversation interface.

Check whether options for Recent Chat History, New Chat, and End Chat are available.

**Actual Result**
No dedicated Recent Chat History option is visible.

No New Chat option is available to start a fresh conversation.

No End Chat option is available to terminate the current conversation.

Users do not have clear controls to manage multiple conversations.

**Expected Result**
**1. Recent Chat History**

Provide an option to view previously created conversations.

Allow users to reopen and continue an existing conversation.

Display conversation titles and timestamps where supported.

**2. New Chat**

Provide a New Chat button.

Clicking it should start a fresh conversation.

Previous conversation messages should not appear in the new chat.

Existing conversation history should remain accessible.

**3. End Chat**

Provide an End Chat option.

Clicking it should end the current conversation.

Display a confirmation message before ending the session if appropriate.

Ensure the conversation history is preserved if history retention is supported.

**Acceptance Criteria**
Recent conversations should be accessible through a dedicated history section.

Users should be able to open previous conversations.

New Chat should create an independent conversation session.

Previous conversation messages should not mix with a new conversation.

End Chat should properly terminate the active conversation.

Existing conversation history should be retained according to the application's session-retention policy.

All chat management controls should be accessible and clearly visible.

Chat management functionality should work consistently across supported agent categories.

**Impact**
Without chat management functionality, users may find it difficult to organize conversations, revisit previous discussions, and start separate sessions for different business queries.

**Priority: High**
**Issue Type: Enhancement / UI Improvement**

**Module: LightRAG – Chatbot / Chat Session Management**

**Environment: QA**

**URL: https://qa-knowledgeforge.dealwallet.com/webui/**

**Reference: Attached screenshot of the Store Manager Chatbot interface.**