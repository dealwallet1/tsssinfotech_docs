**Bug-1**
**Title**
OTP becomes invalid after a single incorrect verification attempt before the 10-minute expiry

**Description**
After a successful signup, an OTP is sent to the user's registered email with a validity period of 10 minutes.

If the user accidentally enters an incorrect OTP (for example, a missing digit or an incorrect character), the API returns an "Invalid or expired OTP" error.

However, when the user immediately retries with the correct OTP (which is still within the 10-minute validity period), the API still returns "Invalid or expired OTP" instead of verifying the OTP successfully.

The OTP should remain valid until it expires or is successfully verified.


**Steps to Reproduce**
1.Sign up with a valid email address.
2.Receive the OTP in the registered email.
3.Enter an incorrect OTP (e.g., one digit is incorrect).
4.Observe that the API returns "Invalid or expired OTP".
5.Before the 10-minute expiry, enter the correct OTP received in the email.
6.Execute the verification request again.

**Actual Result**
1.After one incorrect verification attempt, the OTP becomes unusable.
2.The API returns:
  {
  "detail": "Invalid or expired OTP"
}

3.This happens even though the OTP has not expired.

**Expected Result**
1.An incorrect OTP attempt should return an "Invalid OTP" error only.
2.The original OTP should remain valid until:
     1.the 10-minute expiration time is reached, or
     2.the OTP is successfully verified.
3.Users should be able to retry with the correct OTP within the validity period.

**Environment**
1.API Endpoint: POST /api/v1/auth/verify-otp
2.Environment: Swagger UI
3.Browser: Google Chrome
4.OS: Windows 11

**Notes**
The current behavior can prevent legitimate users from verifying their account if they make a single typing mistake, despite the OTP still being within its 10-minute validity period. The error message is also misleading because the OTP is not expired; it has only been entered incorrectly once.


**Bug-2**
**Title**
Add Confirm Password Field to User Signup Form

**Description:**
The current signup flow only includes a Password field and does not provide a Confirm Password field. Adding a Confirm Password field will help users verify their password before creating an account, reducing the risk of account creation failures due to mistyped passwords.

**Steps to Reproduce**
1.Open the application.
2.Navigate to the Sign Up page.
3.Observe the available input fields.
4.Verify that the form contains:
      1.Full Name
      2.Email
      3.Password
5.Notice that there is no Confirm Password field.
6.Enter valid signup details and submit the form.


**Current Behavior:**
1.Signup form contains:
      1.Full Name
      2.Email
      3.Password
2.No Confirm Password field is available.
3.Users can submit the signup form without re-entering their password.

**Expected Behavior:**
1.Add a Confirm Password field to the signup form.
2.Validate that the Password and Confirm Password values match before submitting the request.
3.Display an appropriate validation message if the passwords do not match.
4.Submit only the password field to the backend API after successful validation (no backend API changes required if confirmPassword is used only for frontend validation).

**Acceptance Criteria:**
1.A Confirm Password field is displayed on the signup page.
2.Password and Confirm Password are mandatory.
3.User cannot proceed if the passwords do not match.
4.Validation message is displayed (e.g., "Passwords do not match.").
5.Signup request is sent only after successful validation.
6.Existing signup functionality continues to work without issues.

**Notes:**
1.The current /api/v1/auth/send-otp API accepts only:
  {
  "fullname": "string",
  "email": "string",
  "password": "string"
}



**Bug-3**
**Title**
Verify OTP API Returns 503 "No Available Server" Instead of Expired OTP Error After OTP Expiry

**Description**
When an OTP has expired (OTP validity is 1 minute) and the user attempts to verify it after the expiry time, the Verify OTP API returns HTTP 503 Service Unavailable with the message "no available server" instead of returning a proper validation error indicating that the OTP has expired.

The API should handle expired OTPs gracefully by returning an appropriate client error (e.g., 400 Bad Request or 401 Unauthorized) along with a meaningful error message.

**Preconditions**
1.User has successfully requested an OTP.
2.OTP validity is configured as 1 minute.

**Steps to Reproduce**
1.Generate an OTP using the Send OTP API.
2.Wait for more than 1 minute until the OTP expires.
3.Enter the expired OTP.
4.Execute the POST /api/v1/auth/verify-otp API request.
5.Observe the response.

**Actual Result**
HTTP Status Code: 503 Service Unavailable
Response Body:
         no available server

**Expected Result**
The API should validate the expired OTP and return an appropriate client error, for example:

1.HTTP Status Code: 400 Bad Request or 401 Unauthorized
2.Response Body:
{
  "message": "OTP has expired"
}

or
{
  "message": "Invalid or expired OTP"
}

3.The API should not return a 503 Service Unavailable response for an expired OTP.

**Impact**
1.Users receive a misleading server error instead of a clear OTP expiry message.
2.Prevents proper client-side error handling.
3.Indicates improper backend exception handling or service routing when processing expired OTPs.


**Bug-4**
**Title**
API Endpoint Displays "no available server" Error Instead of Responding to Requests

**Description:**
When accessing the API endpoint (https://apigarudavpn.dealwallet.com), the application displays the message "no available server" instead of processing the request or returning a valid API response. This indicates that the backend service or API gateway is unavailable.

**Preconditions:**
1.User has access to the API endpoint.
2.Internet connection is active.

**Steps to Reproduce:**
1.Open a web browser.
2.Navigate to https://apigarudavpn.dealwallet.com.
3.Observe the response displayed on the page.

**Actual Result:**
The page displays:
      no available server

**Expected Result:**
The API endpoint should:
1.Return a valid API response (such as JSON), or
2.Display a proper health/status response, or
3.Process API requests successfully without showing a server availability error.

**Impact:**
1.API is inaccessible.
2.Frontend applications depending on this API may fail to function.
3.Users cannot perform any operations that require backend communication.

**Possible Cause:**
1.Backend service is down.
2.API Gateway/Load Balancer cannot route traffic to any healthy backend server.
3.Server deployment failure.
4.Infrastructure or container/service outage.

**Environment:**
1.OS: Windows 11
2.Browser: Microsoft Edge
3.Environment: QA/UAT (apigarudavpn.dealwallet.com)


**Bug-5**
**Title**
Reset Password API Missing confirm_password Field in Request Body

**Description:**
After a user successfully completes the Forgot Password flow and verifies the OTP, the Reset Password API only accepts the following request body:
{
  "email": "string",
  "new_password": "string"
}

The API does not provide or validate a confirm_password field. As a result, there is no backend verification to ensure that the entered password and confirmation password match before updating the user's password.

**Preconditions:**
1.User has initiated the Forgot Password process.
2.OTP has been successfully verified.
3.User is on the Reset Password screen.

**Steps to Reproduce:**
1.Navigate to the Forgot Password flow.
2.Enter a registered email address.
3.Verify the OTP successfully.
4.Open the Reset Password API (POST /api/v1/auth/new-password) in Swagger.
5.Observe the request body schema.

**Actual Result:**
1.The request body contains only:
      1.email
      2.new_password
2.confirm_password field is missing.

**Expected Result:**
1.The Reset Password functionality should include a confirm_password field and validate that:
2.new_password and confirm_password are provided.
3.Both values match before updating the password.
4.If they do not match, the API should return an appropriate validation error.

**Environment:**
1.API Documentation (Swagger)
2.Endpoint: POST /api/v1/auth/new-password

**Impact:**
1.Missing backend validation for password confirmation.
2.Increased risk of incorrect password updates if frontend validation is bypassed.
3.Inconsistent user experience and reduced security.

**Attachments:**
Swagger API screenshot showing the request body schema.

**Note:** If the development team intentionally designed password confirmation to be validated only on the frontend, then this would be an enhancement request rather than a bug. However, from a security and API validation perspective, it is generally recommended that the backend also validate confirm_password (or otherwise ensure password confirmation) instead of relying solely on the client.


**Bug-6**
**Title**
AI returns yearly pricing when user requests monthly subscription plan

**Description:**
When a user explicitly asks for the lowest subscription plan for the monthly pack, the AI response includes both the monthly and yearly prices. The response should respect the user's requested billing cycle and return only the relevant monthly pricing information.

**Steps to Reproduce:**
1.Send the following request:
    {
  "message": "What is the lowest subscription plan for montly pack?",
  "session_id": "user12"
}

2.Observe the AI response.

**Actual Result:**
1.The AI returns the Basic Shield Plan with:
    1.Monthly Price: $4.99
    2.Yearly Price: $49.99 (included even though it was not requested)

**Expected Result:**
1.The AI should return only the details relevant to the monthly subscription plan, including:
      1.Plan name
      2.Monthly price
      3.Applicable features
      4.Other relevant monthly plan information
2.The yearly price should not be included unless the user explicitly asks for yearly pricing or requests both billing options.

**Environment:**
1.Module: Subscription Agent
2.Session ID: user12

**Impact:**
1.The response does not fully align with the user's intent.
2.May cause confusion by presenting information outside the requested billing cycle.
3.Reduces response accuracy and user experience.


**Bug-7**
**Title**
Subscription Agent fails to generate payment link for Premium Yearly plan due to internal tool/function execution error

**Description**
The Subscription Agent fails to process a purchase request for the Premium Yearly subscription. Instead of generating a Stripe payment link, the API returns an internal tool/function execution error while responding with HTTP 200.

**Steps to Reproduce**
1.Open the Swagger documentation.
2.Navigate to the POST /api/v1/agents/chat endpoint.
3.Send the following request:
  {
  "message": "I want to purchase a yearly subscription for the premium plan.",
  "session_id": "user22"
}

4.Click Execute.

**Actual Result**
1.HTTP status code: 200 OK
2.Response contains an internal error:
     1.tool_use_failed
     2.invalid_request_error
     3.Failed to call a function
3.payment_link is returned as null.
4.User is unable to proceed with the subscription purchase.

**Expected Result**
1.The Subscription Agent should identify the Premium Yearly plan.
2.Generate the corresponding Stripe payment link.
3.Return a successful response with a valid payment_link.
4.Internal tool/function errors should not be exposed to the end user.

**Environment**
1.Swagger API
2.Agent Chat API
3.Endpoint: /api/v1/agents/chat

**Impact**
1.Users cannot purchase the Premium Yearly subscription.
2.Subscription purchase flow is blocked.
3.Potential revenue loss due to failed checkout.


**Bug-8**
**Title**
Subscription Plan Detail API returns "No plan found" for existing plan when tier is provided in lowercase

**Description**
The Subscription Plan Detail API fails to retrieve an existing subscription plan when the tier value is provided in lowercase. Although the subscription_plans table contains a plan with the tier value Basic, the API returns a 404 Not Found response for the request using basic.

**Steps to Reproduce**
1.Open the Swagger API.
2.Navigate to POST /api/v1/subscriptions/plan-detail.
3.Send the following request:
  {
  "tier": "basic"
}
4.Execute the request.

**Actual Result**
1.API returns 404 Not Found.
2.Response:
    {
  "detail": "No plan found for tier 'basic'"
}

**Expected Result**
The API should successfully return the Basic subscription plan details even when the tier is provided as basic (lowercase), or it should clearly document that the tier field is case-sensitive.

**Environment**
1.Swagger API
2.Endpoint: POST /api/v1/subscriptions/plan-detail

**Impact**
Users may be unable to retrieve valid subscription plan details due to case-sensitive matching of the tier value, resulting in an incorrect "No plan found" response.

**Evidence**
1.Database contains a subscription plan with tier = "Basic".
2.API request using tier = "basic" returns 404 Not Found.


**Bug-9**
**Title**
Premium Armor pricing card does not display hover highlight effect

**Description:**
The hover highlight effect is inconsistent across the pricing cards. The Basic Shield and Ultimate Aegis cards display a highlighted border when hovered, but the Premium Armor card does not show the same hover effect.

**Steps to Reproduce**
1.Open the Pricing page.
2.Move the cursor over the Basic Shield card.
3.Observe the hover highlight.
4.Move the cursor over the Premium Armor card.
5.Move the cursor over the Ultimate Aegis card.

**Actual Result**
The Premium Armor card does not display the hover highlight/border effect, while the other pricing cards do.

**Expected Result**
All pricing cards (Basic Shield, Premium Armor, and Ultimate Aegis) should display a consistent hover highlight effect when the cursor is placed over them.

**Environment**
1.OS: Windows 11
2.Browser: Google Chrome
3.Module: Pricing Page


**Bug-10**
**Title**
Add Show/Hide Password (Eye Icon) for Password and Confirm Password fields on the Sign Up page

**Description**
The Sign Up form does not provide a Show/Hide Password (eye icon) option for the Password and Confirm Password fields.

Without this functionality, users cannot verify the passwords they have entered, increasing the likelihood of typing errors and failed account creation attempts.

**Steps to Reproduce**
1.Navigate to the Sign Up page.
2.Enter a password in the Password field.
3.Enter a password in the Confirm Password field.
4.Observe the input fields.

**Actual Result**
1.Passwords remain masked.
2.No eye icon is available to view or hide the entered passwords.

**Expected Result**
1.Display an eye icon inside both the Password and Confirm Password fields.
2.Clicking the eye icon should:
3.Show the entered password.
4.Toggle back to a masked password when clicked again.

**Environment**
1.OS: Windows 11
2.Browser: Google Chrome
3.Module: Sign Up

**Classification**
1.If the design/UI specification includes an eye icon: ✅ UI Bug
2.If there is no such requirement in the specification: ✅ Feature Request / UX Enhancement


**Bug-11**
**Title**
Sign Up displays "Failed to fetch" error instead of successful account creation or meaningful error message

**Description**
When a user enters valid registration details and clicks the Sign Up button, the application displays a generic "Failed to fetch" alert instead of creating the account successfully or showing a user-friendly error message.

This results in a poor user experience and does not inform the user about the actual cause of the failure.

**Steps to Reproduce**
1.Navigate to the Sign Up page.
2.Enter a valid Full Name.
3.Enter a valid Email Address.
4.Enter matching Password and Confirm Password.
5.Accept the Terms & Conditions.
6.Click the Sign Up button.

**Actual Result**
1.A browser alert displays "Failed to fetch".
2.The account is not created.
3.No meaningful error message is shown to the user.

**Expected Result**
1.If the registration is successful:
2.Display a success message such as "Account created successfully."
3.Redirect the user to the Login page or OTP verification page (based on the application flow).
4.If registration fails:
5.Display a clear, user-friendly error message explaining the reason (e.g., email already exists, server unavailable, network error, etc.).
6.Do not display the generic "Failed to fetch" alert.

**Environment**
1.Module: Sign Up
2.Browser: Google Chrome
3.OS: Windows 11

**Severity**
High (Prevents users from completing registration)

**Priority**
High

**Possible Root Cause**
1.Backend API is unavailable or returning an error.
2.Frontend is not handling API/network errors properly and is exposing the raw "Failed to fetch" message instead of a meaningful Error


**Bug-12**
**Title**
Remove Device API fails to delete device when device name casing differs and returns "Device not found"

**Description**
1.The Remove Device API returns a 404 - Device not found response when the device name casing is changed (e.g., Pro → pro).
2.The device exists and is returned by the Get Devices API, but the deletion fails due to a case-sensitive name match. The API also exposes a device_id parameter, but the request appears to depend on the device name instead of deleting the device by its unique identifier.

**Steps to Reproduce**
1.Execute the Get Devices API.
2.Verify that a device named iPhone 15 Pro is returned.
3.Open the Remove Device API.
4.Enter the device name as iPhone 15 pro (lowercase p).
5.Click Execute.

**Actual Result**
1.The API returns 404 Not Found.
2.Response:
   {
  "detail": "Device not found"
}

**Expected Result**
1.The API should delete the device using its device_id, regardless of the device name.
2.If deletion by name is supported, the API should clearly document whether name matching is case-sensitive or handle case differences gracefully.
3.The API should return a meaningful validation message if the request parameters are incorrect.

**Environment**
1.Module: Device Management API
2.Endpoint: DELETE /api/v1/devices
3.API Testing Tool: Swagger UI

**Severity**
  Medium

**Priority**
  Medium

**Notes**
If the API is designed to perform a case-sensitive lookup by device name, then the observed behavior is expected and not a bug. However, from an API design perspective, deletion operations should ideally use the device_id (a unique identifier) rather than the device name to avoid failures caused by differences in letter casing.


**Bug-13**
**Title**
Forgot Password – OTP Email Not Received and User Is Not Redirected to OTP Verification Page

**Description:**
When the user enters a registered email address on the Forgot Password page and clicks the Send OTP button, no OTP email is received. Additionally, the application does not redirect the user to the OTP Verification page after submitting the request.

**Preconditions:**
1.User has a registered account.
2.User is on the Forgot Password page.

**Steps to Reproduce:**
1.Open the GarudaVPN login page.
2.Click Forgot Password.
3.Enter a valid registered email address.
4.Click the Send OTP button.
5.Check the registered email inbox (and Spam/Junk folder).

**Actual Result:**
1.No OTP email is received.
2.The user remains on the Forgot Password page.
3.The application does not navigate to the OTP Verification page.

**Expected Result:**
1.An OTP email should be sent successfully to the registered email address.
2.Upon successful OTP generation, the application should automatically redirect the user to the OTP Verification page, where the 3.user can enter the received OTP and continue the password reset process.

**Impact:**
Users cannot proceed with the password reset flow, preventing them from regaining access to their accounts.

**Environment:**
1.Application: GarudaVPN Web Portal
2.Browser: Google Chrome
3.Module: Forgot Password


**Bug-14**
**Title**
Profile page fails to load and displays reload screen after successful login

**Description**
After logging into the application with valid credentials, the user is successfully redirected to the Dashboard. However, when the user clicks on the Profile section from the left navigation menu, the Profile page fails to load and displays a browser error page with the message "This page couldn't load" along with Reload and Back buttons.

**Preconditions**
1.User has a valid GarudaVPN account.
2.User is logged into the application.

**Steps to Reproduce**
1.Open the GarudaVPN web application.
2.Log in using valid credentials.
3.Verify that the Dashboard loads successfully.
4.Click on Profile from the left navigation menu.

**Actual Result**
1.The Profile page does not load.
2.A browser error page is displayed stating:
    "This page couldn't load"
3.User is unable to access the Profile page.

**Expected Result**
1.The Profile page should load successfully and display the user's profile information without requiring a page reload or showing an error.

**Frequency**
100% (Observed consistently)

**Impact**
1.Users cannot access or manage their profile details.
2.Core account management functionality is blocked.

**Environment**
1.Application: GarudaVPN Web Portal
2.Module: Dashboard → Profile
3.Browser: Google Chrome
4.Environment: QA/UAT

**Notes**
1.Check the browser Console for JavaScript errors.
2.Verify whether the Profile API is returning an error (4xx/5xx).
3.Confirm that the routing and frontend navigation to /dashboard/profile are working correctly.


**Bug-15**
**Title**
Quick Connect button redirects to a non-existent page and displays a 404 error

**Description**
After successfully logging into the application, clicking the Quick Connect button redirects the user to the VPN Status page (/dashboard/vpn-status). However, instead of loading the page, the application displays a 404 – This page could not be found error.

**Preconditions**
1.User is logged in with valid credentials.
2.User is on the Dashboard page.

**Steps to Reproduce**
1.Open the GarudaVPN web application.
2.Log in with valid user credentials.
3.Navigate to the Dashboard.
4.Click the Quick Connect button.
5.Observe the redirected page.

**Actual Result**
1.User is redirected to /dashboard/vpn-status.
2.The page displays:
 404 "This page could not be found."
3.The VPN Status page does not load.

**Expected Result**
Clicking Quick Connect should navigate the user to the VPN Status page (or initiate the VPN connection) successfully without displaying a 404 error.

**Frequency**
100% (Occurs every time)

**Environment**
1.Application: GarudaVPN Web Portal
2.Module: Dashboard → Quick Connect
3.Browser: Google Chrome
4.Environment: QA/UAT

**Impact**
1.Users cannot access the VPN Status page through the Quick Connect action.
2.Quick Connect functionality is unusable, preventing users from managing or monitoring VPN connections.


**Bug-16**
**Title**
Purchase Basic button does not redirect to the payment page during subscription purchase

**Description**
A newly registered user without any active subscription is required to purchase a subscription plan before using the VPN service.

Currently, when the user selects a subscription plan (e.g., Basic Shield) and clicks the Purchase Basic button, there is no chatbot-based payment flow.

As per the expected business workflow, all subscription purchases should be processed through the chatbot payment system instead of the current purchase flow.

**Preconditions**
1.User has created a new account.
2.User has no active subscription plan.
3.User is logged into the application.

**Steps to Reproduce**
1.Login with a newly created account.
2.Navigate to Subscriptions.
3.Select Basic Shield (or any available subscription plan).
4.Click Purchase Basic.

**Actual Result**
1.The purchase flow is not routed through the chatbot payment process.
2.Users cannot complete the subscription purchase using the chatbot.

**Expected Result**
1.After clicking Purchase Basic (or any subscription plan), the user should be redirected to the chatbot.
2.The chatbot should guide the user through the payment process.
3.After successful payment, the selected subscription should be activated automatically.

**Business Impact**
1.New users cannot follow the intended chatbot-based subscription purchase flow.
2.Inconsistent payment experience.
3.May prevent users from completing subscription purchases.

**Environment**
1.Application: GarudaVPN Web Portal
2.Module: Subscriptions
3.Browser: Google Chrome
4.Environment: QA/UAT

**Impact**
1.New users are unable to purchase a subscription plan.
2.The subscription purchase flow is blocked, preventing users from upgrading their account.


**Bug-17**
**Title**
Password Reset Allows User to Reuse Current Password as New Password

**Description**
The Password Reset API allows users to set their current password as the new password after successfully completing the Forgot Password (OTP verification) flow. The system updates the password successfully instead of restricting password reuse.

**Environment**
1.Application: GarudaVPN
2.Module: Authentication – Forgot Password / Reset Password
3.Environment: QA
4.API Endpoint: POST /api/v1/auth/new-password

**Preconditions**
1.User has a registered account.
2.User has successfully verified the OTP received via the Forgot Password flow.

**Steps to Reproduce**
1.Log in using a valid email and password.
2.Click Forgot Password.
3.Enter the registered email address and complete OTP verification.
4.On the Reset Password screen, enter the current password in the New Password field.
5.Enter the same current password in the Confirm Password field.
6.Click Submit.

**Actual Result**
1.The password is updated successfully.
2.The API returns:
    {
  "message": "Password updated successfully" 
    }
3.The system allows the user to reuse their existing password as the new password.

**Expected Result**
1.The system should prevent users from reusing their current password.
2.An appropriate validation message should be displayed, such as:
    "New password cannot be the same as the current password."
3.The API should return an appropriate error response (e.g., 400 Bad Request).

**Impact**
1.Allows password reuse, which is a security and validation issue.
2.Does not enforce standard password reset best practices.

**Bug-18**
**Title**
OTP Email Displays Incorrect Expiry Time (10 Minutes Instead of 1 Minute)

**Description**
The OTP email sent to users displays that the OTP is valid for 10 minutes, whereas the actual OTP expiration time configured in the application is 1 minute. This causes inconsistency between the email content and the system behavior.

**Environment**
1.Application: GarudaVPN
2.Module: Authentication – Email OTP Verification
3.Environment: QA

**Preconditions**
User has requested an OTP for registration, login, or password reset.

**Steps to Reproduce**
1.Trigger the OTP generation flow.
2.Open the received OTP email.
3.Observe the OTP validity message in the email.
4.Wait for 1 minute and try to verify the OTP.

**Actual Result**
1.The email displays:
      "This OTP is valid for 10 minutes."
2.However, the OTP expires after 1 minute.

**Expected Result**
1.The OTP validity message in the email should match the actual system configuration.
2.If the OTP expires after 1 minute, the email should display:
           "This OTP is valid for 1 minute."

**Impact**
1.Misleads users about the OTP validity period.
2.Creates confusion when the OTP expires earlier than stated.
3.Results in a poor user experience.


**Bug-19**
**Title**
Frontend AI Chatbot Returns Incorrect Subscription Information Compared to Backend API

**Description**
The frontend AI chatbot returns incorrect information for the same subscription-related query that the backend API answers correctly. This results in inconsistent responses between the frontend and backend.

**Environment**
1.Application: GarudaVPN
2.Module: AI Chatbot
3.Environment: QA

**Preconditions**
1.User is logged in.
2.AI chatbot is accessible.
3.Backend Agents Chat API is available.

**Steps to Reproduce**
1.Call the backend endpoint /api/v1/agents/chat.
2.Ask the following question:
   **"How many devices can connect for yearly plan subscription for Basic Shield?""**
3.Observe the backend response.
4.Open the GarudaVPN web application.
5.Ask the same question in the frontend AI chatbot.
6.Compare both responses.

**Actual Result**
1.Backend API Response:
   1.Returns the correct answer:
         1.Basic Shield yearly plan allows 1 device connection.
2.Frontend Chatbot Response:
   1.States that the Basic Shield plan does not exist.
   2.Indicates no results were found.
   3.Provides incorrect and misleading information.

**Expected Result**
1.The frontend AI chatbot should display the same accurate information returned by the backend API. For this query, it should respond that:
              **"The Basic Shield yearly subscription allows 1 device connection."**
2.The frontend and backend should return consistent responses for identical queries.

**Impact**
1.Users receive incorrect subscription information.
2.Inconsistent behavior between frontend and backend.
3.Reduces trust in the AI chatbot and may mislead users when choosing a subscription plan.


**Bug-20**
**Title**
Profile Displays "Premium Member" for User Without an Active Subscription Plan

**Description**
After logging in with valid credentials, the user is successfully redirected to the dashboard. Although the user does not have an active subscription plan, the profile section in the top-right corner incorrectly displays the account status as "Premium Member".

This creates an inconsistency between the user's actual subscription status and the membership status displayed in the UI.

**Environment**
1.Environment: QA / Staging
2.Module: Dashboard / Profile
3.Browser: Google Chrome
4.Platform: Web

**Preconditions**
1.User account exists.
2.User has no active subscription plan.

**Steps to Reproduce**
1.Open the GarudaVPN application.
2.Log in using valid user credentials.
3.Navigate to the Dashboard.
4.Observe the subscription details.
5.Check the profile section in the top-right corner.

**Actual Result**
1.Current Plan: Free
2.Days Remaining: 0
3.No active subscription
4.However, the profile section displays "Premium Member".

**Expected Result**
1.The membership status shown in the profile should accurately reflect the user's subscription status.

**Examples:**
1.If the user has no active subscription, display "Free Member", "Free Plan", or "No Active Subscription".
2.Display "Premium Member" only when the user has an active premium subscription.

**Impact**
1.Misleading membership information displayed to users.
2.Causes inconsistency between the dashboard and profile.
3.May confuse users about their subscription benefits and account status.


**Bug-21**
**Title**
[Sign Up] Incorrect Button Label Displayed on OTP Verification Screen After User Registration

**Description**
After a user successfully completes the Sign Up form, an OTP is sent to the registered email address. The application redirects the user to the OTP Verification screen. However, the primary action button is incorrectly labeled "Send Reset Link" instead of an OTP verification-related action such as "Verify OTP" or "Verify & Create Account".

This causes confusion because the screen is part of the Sign Up flow, not the Forgot Password flow.

**Module**
Authentication → Sign Up → OTP Verification

**Environment**
1.Environment: QA / Staging
2.Platform: Web
3.Browser: Google Chrome

**Preconditions**
1.User is not registered.
2.User has access to a valid email address.

**Steps to Reproduce**
1.Open the GarudaVPN application.
2.Navigate to the Sign Up page.
3.Enter all mandatory registration details.
4.Click the Sign Up button.
5.Verify that the OTP is successfully received in the registered email.
6.Open the OTP Verification screen.
7.Observe the primary action button.

**Actual Result**
1.The OTP Verification screen displays the button text as:
     "Send Reset Link"
2.even though the user is in the Sign Up OTP verification flow.

**Expected Result**
1.The button label should reflect the current action, for example:
        1.Verify OTP
        2.Verify & Create Account
        3.Continue
        4.Submit OTP
2.The button should not display "Send Reset Link", as this is associated with the Forgot Password workflow.

**Impact**
1.Confuses users during account registration.
2.Creates an inconsistent user experience.
3.May lead users to believe they are in the password reset flow instead of the Sign Up flow.


**Bug-22**
**Title**
AI Chatbot Does Not Provide Subscription Purchase Flow After User Confirms Intent to Buy a VPN Plan

**Description**
When interacting with the AI chatbot to purchase a VPN subscription, the chatbot correctly displays the available subscription plans (Basic, Premium, and Ultimate). However, after the user expresses interest in purchasing a plan and selects or confirms a plan (e.g., Basic Plan), the chatbot only continues to provide plan information and asks whether the user would like to purchase it. It does not proceed with the subscription purchase workflow by providing a payment link, checkout page, or purchase action.

This prevents users from completing the subscription purchase directly through the chatbot.

**Preconditions**
1.User is logged into the GarudaVPN dashboard.
2.AI Chatbot (Aegis AI Support) is available.

**Steps to Reproduce**
1.Log in to the GarudaVPN dashboard.
2.Open the Aegis AI Support chatbot.
3.Type "I want to buy the VPN subscription plan."
4.Observe that the chatbot lists the available plans.
5.Type "Basic" (or any available plan).
6.When prompted, reply "Yes" to confirm the purchase.
7.Observe the chatbot response.

**Actual Result**
1.The chatbot repeatedly displays subscription plan details and pricing.
2.The chatbot asks if the user wants to purchase the selected plan but does not initiate the purchase process.
3.No payment page, checkout link, payment button, or subscription activation flow is provided.

**Expected Result**
After the user confirms the purchase:
     1.The chatbot should initiate the subscription purchase flow.
     2.It should provide a Checkout/Payment button or redirect the user to the subscription payment page.
     3.The selected plan should be carried forward to the payment process.
     4.The user should be able to complete the subscription without leaving the chatbot flow.

**Environment:**
1.Environment: QA / Staging
2.Browser: Google Chrome
3.OS: Windows 11

**Impact**
1.Users cannot purchase a VPN subscription through the chatbot.
2.The conversation reaches a dead end after purchase confirmation.
3.Results in poor user experience and potential loss of subscription conversions.

**Possible Cause**
1.Chatbot intent for purchase confirmation is not mapped to the checkout/payment workflow.
2.Missing backend integration between the AI chatbot and the subscription/payment service.
3.Purchase action or payment redirect API is not being triggered after user confirmation.


**Bug -23**
**Title**
OTP Expiry Forces User to Re-enter Registration Details Instead of Allowing OTP Resend

**Description:**
When the OTP expires during the signup process, the application displays an "Invalid or expired OTP" alert. After dismissing the alert, the user has no option to resend a new OTP and is forced to navigate back and re-enter all registration details (email, password, etc.) to restart the signup process.
This creates unnecessary effort and negatively impacts the user experience.

**Steps to Reproduce:**
1. Navigate to the Sign Up page.
2. Enter a valid email address and password.
3. Request an OTP.
4. Wait until the OTP expires (or enter an expired OTP).
5. Click the Verify button.

**Actual Result:**
* A popup displays "Invalid or expired OTP."
* No Resend OTP option is available.
* User must return to the signup page and re-enter all registration details to receive a new OTP.

**Expected Result:**
* When the OTP expires, the application should:
   * Display an appropriate inline message such as "Your OTP has expired. Please request a new OTP."
   * Provide a Resend OTP button/link on the OTP verification page.
   * Retain the previously entered email address and password.
   * Send a new OTP without requiring the user to restart the registration process.

**Suggested Enhancement:**
* Add a Resend OTP link/button below the OTP input field.
* Optionally include a countdown timer (e.g., Resend OTP in 30 seconds) to prevent excessive OTP requests.
* Keep the user on the OTP verification screen until verification is completed successfully.

**Environment:**
* Application: Garuda VPN
* Module: Sign Up – OTP Verification
* Environment: Web
* Browser: Chrome (as per screenshot)

**Impact:**
* Poor user experience.
* Increased signup abandonment.
* Unnecessary repetition of registration steps.
* Higher support burden due to failed registrations.


**Bug -24**
**Title**
User Can Purchase Subscription Through Chatbot Without Authentication

**Description**
A user who is not logged in can purchase a subscription plan through the AI chatbot. The chatbot displays the subscription details, redirects the user to the payment gateway, and the payment is completed successfully without requiring user authentication.

This allows anonymous users to purchase subscription plans, which bypasses the application's authentication flow and poses a serious security and business logic issue.

**Preconditions**
1.User is not logged in.
2.AI Chatbot is accessible.

**Steps to Reproduce**
1.Open the GarudaVPN website.
2.Do not log in.
3.Open the AI Chatbot.
4.Enter: "I want to purchase Basic monthly subscription plan."
5.Observe that the chatbot displays the subscription plan details.
6.Click Continue to Secure Payment.
7.Complete the payment process.

**Actual Result**
1.The chatbot allows the user to proceed with payment without authentication.
2.Payment is processed successfully.
3.The subscription purchase completes even though the user is not logged in.

**Expected Result**
1.The chatbot should verify whether the user is authenticated before initiating the subscription purchase.
2.If the user is not logged in, the chatbot should display a message such as:
        **"Please log in to your account before purchasing a subscription plan."**
3.The Continue to Secure Payment button should either be disabled or redirect the user to the login page.
4.Payment should not be initiated for unauthenticated users.

**Environment:**
1.Application: GarudaVPN
2.Module: AI Chatbot
3.Browser: Google Chrome
4.Environment: QA

**Impact**
1.Authentication bypass.
2.Unauthorized subscription purchases.
3.Subscription may not be associated with a valid user account.
4.Potential payment reconciliation and account management issues.
5.High security and business logic risk.

**Suggested Fix**
1.Validate the user's authentication status before displaying payment options.
2.Restrict access to the payment gateway for unauthenticated users.
3.Enforce backend authentication checks before creating a Stripe checkout session or processing any subscription payment.


**Bug -25**
**Title**
Chatbot responds to general knowledge questions instead of restricting responses to GarudaVPN-related queries

**Description**
The Aegis AI Support chatbot currently answers general knowledge questions that are unrelated to the GarudaVPN application. For example, when asked "capital of india", the chatbot responds with "The capital of India is New Delhi."

The chatbot should be restricted to answering only GarudaVPN-related queries, account support, subscriptions, billing, devices, troubleshooting, and knowledge base content. Any unrelated/general-purpose questions should be declined with an appropriate message.

**Steps to Reproduce**
1.Log in to the GarudaVPN Dashboard.
2.Open the Aegis AI Support chatbot.
3.Enter a general knowledge question (e.g., "capital of india").
4.Submit the query.
5.Observe the chatbot response.

**Actual Result**
The chatbot answers the general knowledge question correctly (e.g., "The capital of India is New Delhi."), even though it is unrelated to GarudaVPN.

**Expected Result**
1.The chatbot should not answer general knowledge or unrelated questions.
2.It should respond with a message such as:
  **"I'm designed to assist only with GarudaVPN-related questions, including subscriptions, billing, devices, account management, and technical support. Please ask a GarudaVPN-related question."**

**Impact**
1.Users may use the chatbot as a general-purpose AI assistant instead of a product support assistant.
2.Increased unnecessary AI usage and token consumption.
3.Inconsistent with the intended chatbot scope and business requirements.
4.May lead to irrelevant conversations and reduced support efficiency.

**Environment:**
1.Application: GarudaVPN Dashboard
2.Module: Aegis AI Support Chatbot
3.Environment: QA
4.Browser: Google Chrome
5.OS: Windows 11

**Suggested Fix**
1.Implement domain-specific intent filtering or prompt guardrails.
2.Restrict responses to GarudaVPN knowledge base and support documentation.
3.Reject or redirect unrelated queries with a predefined fallback message.
4.Add backend validation to prevent responses outside the allowed knowledge domain.


**Bug -26**
**Title**
Change Password button is unresponsive after successful OTP verification

**Description**
After successfully verifying the OTP for password reset, the user enters the current password, new password, and confirm password. However, clicking the "Change Password" button does not trigger any action. The password is not updated, and no success or error message is displayed.

**Environment**
1.Application: GarudaVPN Web
2.Module: Forgot Password / Reset Password
3.Environment: QA
4.Browser: Google Chrome
5.OS: Windows 11

**Preconditions**
1.User account is registered.
2.User has successfully completed OTP verification.

**Steps to Reproduce**
1.Navigate to the Forgot Password page.
2.Enter a registered email address.
3.Request and verify the OTP successfully.
4.Enter the following:
    1.Current Password
    2.New Password
    3.Confirm Password
5.Click the Change Password button.

**Expected Result**
1.The Change Password button should be clickable and submit the password reset request.
2.If the entered details are valid, the password should be updated successfully.
3.A success message should be displayed, and the user should be redirected to the login page (or appropriate page).
4.If validation fails, an appropriate error message should be shown.

**Actual Result**
1.Clicking the Change Password button does not perform any action.
2.No API request appears to be triggered.
3.No success or error message is displayed.
4.The user remains on the same page, making it impossible to complete the password reset process.

**Impact**
1.Users cannot complete the password reset process even after successful OTP verification.
2.Prevents users from regaining access to their accounts.
3.Results in a broken password recovery flow.


**Bug -27**
**Title**
Dashboard Displays Only One Active Subscription While Backend Returns Multiple Active Subscriptions

**Description**
After purchasing Basic Shield Monthly and Ultimate Shield Monthly using the same account, the backend API returns both subscriptions with status: active.

However, the Dashboard UI displays only the Ultimate Shield plan as the current subscription, while the Basic Shield subscription is missing from the active subscriptions view.

This results in an inconsistency between the frontend and backend.

**Preconditions**
1.User is logged in.
2.User has successfully purchased:
3.Basic Shield Monthly
4.Ultimate Shield Monthly

**Steps to Reproduce**
1.Log in to the application.
2.Purchase the Basic Shield Monthly subscription.
3.Purchase the Ultimate Shield Monthly subscription using the same account.
4.Open the Dashboard.
5.Verify the Overview and Subscriptions sections.
6.Verify the backend API response (GET /api/v1/subscriptions/my-subscriptions).

**Actual Result**
1.Backend API returns two active subscriptions:
2.Basic Shield (Active)
3.Ultimate Shield (Active)
4.Dashboard displays only Ultimate Shield.
5.Basic Shield is not shown in the UI.

**Expected Result**
1.The Dashboard should accurately reflect the backend data.
**If multiple active subscriptions are supported, both active subscriptions should be displayed with their respective plan details and validity periods.**

**Impact**
1.Frontend is inconsistent with backend data.
2.Users cannot view all their active subscriptions.
3.Creates confusion regarding purchased plans.
4.Increases customer support requests.

**Evidence**
**Backend API Response:**
1.Basic Shield → status: active
2.Ultimate Shield → status: active

**Frontend:**
1.Displays only Ultimate Shield as the current plan.
2.Billing/Invoices correctly display both purchases.


**Bug -28**
**Title**
Frontend Chatbot Displays Incorrect and Inconsistent Subscription Details Compared to Backend API Response

**Description**
The frontend chatbot returns a different response than the backend API for the same user query.

**Preconditions**
1.User has a valid GarudaVPN account.
2.User is logged in to the GarudaVPN web application.
3.The AI Chatbot is accessible and operational.
4.The backend /api/v1/agents/chat API is available and responding successfully.
5.The user has at least one active subscription (to compare chatbot subscription information with the Subscription page).
6.Swagger API documentation is accessible for backend response verification.

**Steps to Reproduce**
1.Log in to GarudaVPN.
2.Open the chatbot.
3.Ask:
    **कितने सब्सक्रिप्शन प्लान हैं?**
4.Compare the frontend chatbot response with the backend /api/v1/agents/chat API response.

**Actual Result**
1.Backend correctly returns only the available subscription plans (Basic, Premium, Ultimate).
2.Frontend chatbot additionally displays current subscription information and purchase suggestions.
3.The chatbot states the user has multiple active subscriptions (Basic and Ultimate), which does not match the subscription page.
4.The frontend response is inconsistent with the backend response.

**Expected Result**
1.The frontend chatbot should accurately display the backend response.
2.It should only answer the user's question by listing the available subscription plans.
3.It should not append incorrect or unrelated subscription information unless explicitly requested and verified.

**Environment**
1.Frontend: GarudaVPN Web Application
2.Backend: /api/v1/agents/chat
3.Browser: Chrome
4.Module: AI Chatbot

**Impact**
1.Users receive different responses for the same question in the frontend and backend, causing inconsistency.
2.The chatbot displays incorrect or misleading subscription information, which can confuse users about their active plans.
3.Users may believe they have multiple active subscriptions or incorrect plan details.
4.This reduces trust in the AI chatbot and the accuracy of the application.
5.Inconsistent frontend and backend behavior can lead to unnecessary customer support requests and a poor user experience.


**Bug -29**
**Title**
Agent Chat API returns 524 Origin Timeout for chat requests

**Description**
The Agent Chat API is returning a 524 Origin Timeout when a valid chat request is submitted through Swagger. The request reaches the server successfully, but the backend does not respond within Cloudflare's 120-second timeout limit.

**Environment**
1.Application: GarudaVPN API
2.Module: Agent Chat API
3.Environment: QA/UAT
4.API Endpoint: POST /api/v1/agents/chat
5.Tested Via: Swagger UI

**Preconditions**
1.User is logged in.
2.Valid Bearer Token is provided.
3.Swagger API is accessible.

**Steps to Reproduce**
1.Open the Swagger documentation.
2.Authorize using a valid Bearer Token.
3.Navigate to POST /api/v1/agents/chat.
4.Enter the following request body:
  **{
  "message": "ಬೆಳಗಾವಿ ಯಾವ ಜಿಲ್ಲೆಗೆ ಸೇರಿದೆಂದು ತಿಳಿಸಿ",
  "session_id": "user24"
}**

5.Click Execute.
6.Wait for the response.

**Actual Result**
1.API returns HTTP Status Code: 524
Error:
   **Error: response status is 524
   Error 524: A timeout occurred**
2.Response indicates:
  1.Origin server did not return a complete response.
  2.Cloudflare Proxy Read Timeout (120 seconds).
  3.origin_response_timeout

**Expected Result**
1.The API should process the chat request successfully and return:
  1.HTTP 200 OK
  2.Chatbot response containing the answer to the user's query.
3.If backend processing fails, it should return a proper application error (e.g., 500 Internal Server Error or 503 Service Unavailable) with a meaningful message instead of timing out.

**Impact**
1.Users are unable to receive chatbot responses.
2.Chat functionality becomes unavailable.
3.Causes poor user experience and API reliability issues.
4.Automated API tests fail due to request timeout.

**Evidence**
1.Valid request payload submitted through Swagger.
2.API request executed successfully.
3.Server responded with 524 Origin Timeout after exceeding the backend processing time.
4.Screenshot attached showing the request payload and the 524 timeout response.


**Bug -30**
**Title**
Dashboard displays incorrect "Days Remaining" when multiple active subscription plans exist

**Description**
When a user has multiple active subscription plans purchased on different dates, the Dashboard correctly displays 2 Active Plans, but the Days Remaining widget shows only 27 days.

The dashboard appears to calculate the remaining days based on only one subscription instead of accurately reflecting the active subscriptions or clearly indicating which subscription the countdown belongs to.

**Preconditions**
1.User account is logged in.
2.User has purchased two active subscription plans.
3.Basic Shield purchased on 13/07/2026
4.Ultimate Shield purchased on 14/07/2026
5.Both subscriptions are active.

**Steps to Reproduce**
1.Log in with a user account having two active subscriptions.
2.Navigate to the Dashboard/Overview page.
3.Verify the Active Plans section.
4.Observe the Days Remaining card.

**Actual Result**
1.The dashboard correctly shows 2 Active Plans.
2.The Days Remaining section displays 27 days without indicating which subscription it belongs to.
3.The displayed value does not accurately represent the remaining validity of both active subscriptions.

**Expected Result**
1.The dashboard should correctly handle multiple active subscriptions by implementing one of the following:
2.Display remaining days for each active subscription separately, or
3.Clearly indicate that the displayed countdown belongs to a specific subscription (e.g., Basic Shield – 27 Days Remaining), or
4.Display the correct overall subscription validity based on the application's business logic.
5.The remaining days should always be consistent with the subscription purchase/expiry dates.

**Impact**
1.Misleading subscription information is displayed to users.
2.Users cannot determine which subscription the remaining days refer to.
3.May cause confusion regarding subscription validity and renewal dates.
4.Reduces trust in the subscription management dashboard.

**Environment**
1.Module: Dashboard / Overview
2.Feature: Subscription Summary
3.Platform: Web
4.Browser: Chrome (as observed)

**Evidence:**
1.2 Active Plans (Ultimate Shield & Basic Shield)
2.Days Remaining: 27
3.Invoice dates: 13/07/2026 and 14/07/2026


**Bug -31**
**Title**
Backend cannot retrieve subscription purchase dates when users request subscription history

**Description**
When a user asks for the dates on which subscription plans were purchased (e.g., "In which dates I have taken subscription plans?"), the chatbot is unable to retrieve the historical purchase dates.

Instead, the backend responds that it cannot access historical subscription data, preventing the chatbot from answering the user's question accurately.

**Preconditions**
1.User is logged in.
2.User has one or more subscription purchases.
3.Subscription purchase history exists.

**Steps to Reproduce**
1.Open the chatbot.
2.Ask:
   **"In which dates I have taken subscription plans?"**
3.Observe the backend response.

**Actual Result**
1.The backend returns:
**"I cannot access historical subscription dates for users. My capabilities are limited to checking current subscription status..."**
2.As a result, the chatbot cannot provide the subscription purchase dates.

**Expected Result**
1.The backend should retrieve the user's subscription purchase history and return the purchase dates, for example:
   1.Basic Shield – Purchased on 13/07/2026
   2.Ultimate Shield – Purchased on 14/07/2026
2.This allows the chatbot to answer the user's question accurately.

**Impact**
1.Users cannot obtain their subscription purchase history through the chatbot.
2.The chatbot cannot answer account-history-related questions despite the data existing elsewhere in the system.
3.Results in inconsistent or incomplete user experience.


**Bug -32**
**Title**
Telegram Bot does not allow users to log out after successful login

**Description**
After successfully logging into the Telegram bot using valid credentials and OTP verification, the user is unable to log out. When the /logout <email> command is entered, the bot responds:
**"I'm sorry, but I can't log you out directly. Please use the GarudaVPN app or website to log out, or raise a ticket if you need further assistance."**

This prevents users from ending their authenticated session within the Telegram bot.

**Preconditions**
1.User has a valid registered account.
2.Telegram bot is accessible.
3.User is not logged in before starting the test.

**Steps to Reproduce**
1.Open the Telegram bot.
2.Enter the login command with a valid email.
3.Receive the OTP.
4.Enter the correct OTP.
5.Verify that the login is successful.
6.Enter the logout command (e.g., /logout <email>).

**Actual Result**
1.The bot does not log out the user and instead displays:
**"I'm sorry, but I can't log you out directly. Please use the GarudaVPN app or website to log out, or raise a ticket if you need further assistance."**

**Expected Result**
1.The bot should:
  1.Successfully log out the authenticated user and confirm the logout (e.g., "You have been logged out successfully."), or
  2.If logout is intentionally unsupported, this limitation should be clearly documented and users should not be allowed to create authenticated sessions that cannot be terminated from the bot.

**Impact**
1.Users cannot end their authenticated session from the Telegram bot.
2.Poor user experience due to inconsistent authentication flow.
3.Potential security concern if users expect to be able to terminate their session on shared devices.

**Severity**
Medium

**Priority**
Medium

**Environment**
1.Platform: Telegram Bot
2.Authentication: Email + OTP
3.Browser/OS: N/A (Telegram client)


**Bug -33**
**Title**
Chat API does not recognize valid JWT token after successful login

**Description**
After successfully logging in through the /api/v1/auth/login API, a valid JWT access token is returned with a 200 OK response. The token is then passed in the Authorization: Bearer <JWT_TOKEN> header while calling the /api/v1/agents/chat API.

However, the Chat API does not recognize the authenticated user and returns the response:

**"Please login first. Send: /login your@email yourpassword"**

This indicates that the JWT authentication/session is not being properly recognized or maintained between the Login API and Chat API.

**Preconditions**
1.Valid user account exists.
2.User credentials are valid.
3.Login API is available.
4.JWT Bearer authentication is configured.

**Steps to Reproduce**
1.Call POST /api/v1/auth/login with valid email and password.
2.Verify that the API returns 200 OK.
3.Copy the access_token JWT from the login response.
4.Authorize the API using the JWT token through Swagger UI.
5.Call POST /api/v1/agents/chat.
6.Provide a valid chat request, for example:
   {
  "message": "What is my current subscription plans?",
  "session_id": "user253"
}
7.observe the API response.

**Expected Result**
1.The Chat API should recognize the valid JWT token and process the user's question successfully.
Example:
  {
  "response": "Your current subscription plan is...",
  "session_id": "user253"
}

**Actual Result**
1.The Chat API returns:
    {
  "response": "Please login first. Send: /login your@email yourpassword",
  "session_id": "user253",
  "agent_used": null,
  "tools_used": [],
  "payment_link": null
}

**Impact**
1.Authenticated users cannot access the Chat API after successful login.
2.The JWT authentication flow is inconsistent between the Login API and Chat API.
3.Users are incorrectly treated as unauthenticated.
4.Chat functionality requiring authenticated user information cannot be used.


**Bug -34**
**Title**
Chatbot provides incorrect device limit for Ultimate Monthly subscription in Hindi Language

**Description**
When a user asks the chatbot in Hindi about the device limit for the Ultimate Monthly Plan, the chatbot provides an incorrect response stating that the plan has a maximum device limit of 1.

However, the actual subscription details show that the Ultimate Plan supports Unlimited device connections.

**Preconditions**
1.User is logged in.
2.User has an active Ultimate Monthly Plan subscription.
3.Chatbot is available.
4.Hindi language input is supported.

**Steps to Reproduce**
1.Log in with a user account having an active Ultimate Monthly Plan.
2.Navigate to the Subscriptions page.
3.Verify that the Ultimate Plan shows Devices: Unlimited.
4.Open the chatbot.
5.Ask the following question in Hindi:
  **"अल्टीमेट मंथली प्लान सब्सक्रिप्शन के लिए डिवाइस की कितनी लिमिट है?"**
6.Observe the chatbot response.

**Expected Result**
1.The chatbot should provide the correct information based on the user's actual subscription plan:
   **The Ultimate Monthly Plan supports unlimited device connections.**
2.The response should remain accurate regardless of the language used by the user.

**Actual Result**
The chatbot incorrectly responds that the Ultimate Monthly Plan has a device limit of 1.

**Impact**
1.Users receive incorrect subscription information.
2.The chatbot response does not match the actual plan configuration.
3.This can cause confusion regarding the user's subscription benefits.
4.Multilingual chatbot responses may be using incorrect or outdated plan data.


**Bug -35**
**Title**
Profile update fails with "Failed to update profile" error after clicking Save Changes

**Description**
When a logged-in user attempts to update their profile information from the Profile page and clicks the Save Changes button, the application displays the error message "Failed to update profile." The profile information is not updated successfully.

**Preconditions**
1.User is logged into the application.
2.User is on the Dashboard → Profile → Personal Information page.
3.User account is active.

**Steps to Reproduce**
1.Log in with valid user credentials.
2.Navigate to Dashboard → Profile.
3.Modify one or more editable profile fields (e.g., Full Name or Phone Number).
4.Click the Save Changes button.

**Actual Result**
1.A popup appears with the message: 
   **Failed to update profile.**
2.The updated profile information is not saved.

**Expected Result**
1.The profile information should be updated successfully.
2.A success confirmation message (e.g., "Profile updated successfully.") should be displayed.
3.The updated values should persist after refreshing the page.

**Impact**
1.Users are unable to update their personal information.
2.Prevents users from maintaining accurate profile details.
3.Degrades overall user experience.

**Severity**
High

**Priority**
High

**Environment**
1.Application: GarudaVPN Web Portal
2.Module: Dashboard → Profile
3.Browser: Google Chrome
4.OS: Windows 11


**Bug -36**
**Title**
Frontend chatbot resets to a new chat instead of displaying the "Please login first" response for unauthenticated users

**Description**
When an unauthenticated user asks a subscription-related question in the chatbot, the backend correctly responds with a login prompt. However, the frontend chatbot does not display this response. Instead, it keeps loading and then resets the conversation to a fresh chat with the default welcome message and suggested prompts.

This results in inconsistent behavior between the backend API and the frontend chatbot.

**Preconditions**
1.User is not logged in.
2.GarudaVPN website is open.
3.AI chatbot is available.
4.Backend API is accessible.

**Steps to Reproduce**
1.Open the GarudaVPN website without logging in.
2.Open the AI chatbot.
3.Enter a subscription-related query (e.g., "I want to purchase basic monthly subscription plan?").
4.Observe the frontend chatbot behavior.
5.Execute the same request through the backend Swagger API.

**Actual Result**
1.Backend: Returns the expected response:
    **"Please login first. Send: /login your@email yourpassword"**
2.Frontend: Displays a loading indicator and then resets the chat to a fresh conversation with the default welcome message instead of showing the backend response.

**Expected Result**
1.The frontend should display the backend response exactly as returned:
 **"Please login first. Send: /login your@email yourpassword"**
2.The chat session should remain intact and should not reset to a new conversation.
3.Backend Response (Verified)
4.HTTP Status: 200 OK
5.Response:
      {
  "response": "Please login first. Send: /login your@email yourpassword",
  "session_id": "...",
  "agent_used": null,
  "tools_used": [],
  "payment_link": null
}

**Environment**
1.Platform: Web
2.Module: AI Chatbot
3.Authentication State: Not Logged In
4.Browser: Google Chrome (Windows)

**Impact**
1.Users do not receive the required login instruction.
2.Conversation context is lost due to the chat reset.
3.Inconsistent behavior between frontend and backend.
4.Poor user experience and confusion during subscription flow.