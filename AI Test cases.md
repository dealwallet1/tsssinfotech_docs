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

All four agent functionalities reviewed.

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