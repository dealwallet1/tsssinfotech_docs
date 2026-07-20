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