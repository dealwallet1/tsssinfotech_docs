**Testcase 1**
**Title**: Sign Up Fails With Database Query Error When Creating a New Account

**Description**
When a user enters valid registration details and clicks the Sign Up button, the account creation process fails.
Instead of successfully creating the account, the application displays a backend/database error:
**Failed query: select "id", "name", "email", "email_verified", "image", "phone", "phone_verified", "role", "is_anonymous", "is_super_admin", "raw_app_meta_data", "raw_user_meta_data", "created_at", "updated_at", "last_sign_in_at", "banned_until", "deleted_at" from "user" where "user"."email" = $1 limit $2**
The error indicates that the application is failing while querying the user table during the registration process.

**Preconditions**
User is not already registered with the provided email address.
User has access to the DealWallet Sign Up page.
Internet connection is available.
Sign Up page is accessible.
Valid registration details are available.

**Steps to Reproduce**
Navigate to the DealWallet Sign Up page.
Enter a valid Username.
Enter a valid Email address.
Enter a valid Password.
Enter the same password in Confirm Password.
Accept the Terms & Conditions checkbox.
Complete the Cloudflare verification.
Click the Sign Up button.
Observe the application response.

**Actual Result**
The account is not created.
A database/backend error popup is displayed showing a failed SQL query against the user table.

**Example error:**
Failed query:
select "id", "name", "email", "email_verified",
"image", "phone", "phone_verified", "role",
"is_anonymous", "is_super_admin",
"raw_app_meta_data", "raw_user_meta_data",
"created_at", "updated_at", "last_sign_in_at",
"banned_until", "deleted_at"
from "user"
where "user"."email" = $1
limit $2

**Expected Result**
**When valid registration details are provided and the user clicks Sign Up:**
The request should be processed successfully.
The backend should successfully validate whether the email already exists.
A new user account should be created.
The user should receive the appropriate success/verification message.
The user should be redirected to the next expected step, such as email/OTP verification or the application dashboard.
Database/SQL errors should not be exposed to the end user.

**Priority**
High

**Reason: This issue prevents users from creating new accounts and blocks the complete registration flow.**

**Labels**
bug
authentication
signup
registration
backend
database
high-priority

**Environment**
**Item	                                 Details**
Application                          	DealWallet
Page	                                /signup
Browser	                                Google Chrome
OS	                                    Windows
Environment	                            QA/Testing
Feature	                                User Registration / Sign Up
Database	                            User table involved
Date Observed	                        29-Sep-2026

**Impact**
**User Impact: High**
New users cannot complete registration.
Account creation is blocked.
Users are exposed to an internal database error.
This can prevent new customers from accessing the application.
The displayed SQL query may expose internal database/schema information and therefore should not be shown to end users.

**Evidence**
**screenshot attached: The provided screenshot shows:**
Valid registration details entered.
Terms & Conditions accepted.
Cloudflare verification completed.
Sign Up button clicked.
Backend/database query error displayed in the top-right notification.

**Testcase 2**
**Title**:Discover More card subtitle text is inconsistently positioned

**Description:**
In the Home page Discover More section, the supporting text “Fresh guides and real shopper conversations are one click away.” is not consistently aligned within the card. Its position appears visually unbalanced compared with the main heading and the Blog/Forum cards.

**Preconditions:**
User can access the DealWallet Home page.
Home page is loaded successfully.
Navigate/scroll to the Discover More section.

**Steps to Reproduce:**
Open the DealWallet Home page.
Scroll down to the Discover More section.
Observe the text “Fresh guides and real shopper conversations are one click away.”
Compare its position/alignment with the “New here? There's more to explore.” heading and the Blog/Forum cards.
Resize the browser if required and observe the positioning.

**Actual Result:**
The supporting text is positioned inconsistently within the Discover More section. The vertical alignment does not look properly balanced with the main heading and surrounding content.

**Expected Result:**
The supporting text should have a consistent and intentional alignment within the Discover More card, maintaining proper spacing and vertical positioning relative to the main heading and the Blog/Forum cards.

**Priority:**
Medium

**Labels:**
bug, ui, alignment, home-page, responsive-ui

**Environment:**
Application: DealWallet
Page: Home
Browser: Google Chrome
OS: Windows
Environment: QA
Screen resolution: As shown in attached screenshot

**Impact:**
The issue does not block functionality, but it affects the visual consistency, layout quality, and overall UI polish of the Home page.

**Evidence:**
Attached screenshot showing the Discover More section and the inconsistent positioning of the supporting text.