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

2.The Confirm Password field is intended for frontend validation only and does not need to be included in the API request unless backend requirements change.