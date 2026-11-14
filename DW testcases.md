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
Attached screenshot showing the Discover More section and the inconsistent positioning of the supporting text..

**Testcase 3**
**Title**:Improve Flash Sale Section: Move “Ends In” Countdown to Banner and Update Flash Sale Icon

**Description**
On the DealWallet Home page, the Flash Sale section requires two UI improvements:

1.Move the **“Ends In” countdown**into a full-width Flash Sale banner/header instead of displaying it separately above the product cards.
2.Replace the existing Flash Sale icon with the **⚡ lightning icon** to provide a clearer visual representation of a limited-time sale.
3.The countdown should clearly indicate that the timer applies to the **entire Flash Sale section**, while the product cards should remain clean and uncluttered.

**Preconditions**
1.User can access the DealWallet Home page.
2.Flash Sale section is available.
3.Flash Sale contains active products.
4.Flash Sale countdown is active.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the **Flash Sale section**.
3.Observe the current Flash Sale icon.
4.Observe the current **“Ends In”** countdown.
5.Observe the position of the countdown relative to the Flash Sale heading and product cards.

**Actual Result**
1.The Flash Sale section currently uses the existing star-style icon.
2.The **“Ends In”** countdown is displayed separately above the product cards.
3.The countdown appears visually detached from the Flash Sale heading.
4.The product section does not clearly communicate that the countdown applies to the complete Flash Sale section.

**Expected Result**
**1. Flash Sale Icon**
Replace the current Flash Sale icon with:

**⚡ Flash Sale**

The lightning icon should be positioned consistently with the Flash Sale heading.

Example:
**⚡ Flash Sale**

**2. Flash Sale Countdown**
Move the countdown into a **full-width Flash Sale banner/header.**

Recommended layout:
┌─────────────────────────────────────────────────────────────┐
│ ⚡ Flash Sale                                      View All│
│                                                             │
│ 🔴 Ends in 01:47:23   Hurry! Limited Time Deals        →   │
└─────────────────────────────────────────────────────────────┘

   Product 1       Product 2       Product 3       Product 4
   ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐
   │  Image  │     │  Image  │     │  Image  │     │  Image  │
   │  Name   │     │  Name   │     │  Name   │     │  Name   │
   │  Price  │     │  Price  │     │  Price  │     │  Price  │
   │ Buy Now │     │ Buy Now │     │ Buy Now │     │ Buy Now │
   └─────────┘     └─────────┘     └─────────┘     └─────────┘

**Priority**
**Medium**

**Labels**
qa
ui
ux
frontend
home-page
flash-sale
countdown
visual-improvement

**Environment**
**Field	                                        Details**
Application	                                   DealWallet
Module	                                       Home Page
Section	                                       Flash Sale
Browser	                                       Google Chrome
OS	                                           Windows
Environment	                                   QA
View	                                       Desktop
Feature	                                       Flash Sale

**Impact**
**Medium – UI/UX**

**These changes will improve:**
1.Visual hierarchy of the Flash Sale section.
2.Visibility of the limited-time countdown.
3.Understanding that the countdown applies to the Flash Sale.
4.Product-card cleanliness.
5.Consistency of the Flash Sale branding.
6.Overall professional appearance of the Home page.

**Evidence**
**Current issue**: Existing DealWallet Home page screenshot showing the current Flash Sale icon and separate “Ends In” countdown.

**Proposed change:**
**Option 4 — Full-width Flash Sale banner + ⚡ Flash Sale icon + countdown inside the banner.**

**Testcase 4**
**Title**:Home Page Sections Are Cut Off and Content Is Not Fully Rendered

**Description**
On the DealWallet Home page, multiple sections are not displayed correctly. The page appears to have cut-off/incomplete content, with large blank spaces between sections and a red horizontal element appearing without the expected content around it.

The affected sections visible in the screenshot include:

1.Flash Sale
2.Thundering Deal
3.Popular Stores
4.Best Credit Cards
The page does not appear to render the complete content for these sections, resulting in an incomplete and visually broken Home page.

**Preconditions**
1.User can access the DealWallet Home page.
2.Home page loads successfully.
3.Required Home page sections/data are available.
4.Browser window is opened in desktop view.

**Steps to Reproduce**
1.Open the DealWallet website.
2.Navigate to the **Home** page.
3.Scroll down through the Home page.
4.Observe the sections after the initial Home page content.
5.Check the **Flash Sale, Thundering Deal, Popular Stores**, and **Best Credit Cards sections**.
6.Observe the content and spacing between these sections.

**Actual Result**
1.Home page sections appear **cut off/incomplete.**
2.Large empty spaces are visible between sections.
3.**Thundering Deal** is displayed, but its expected content is missing.
4.A large red horizontal element is displayed without the expected surrounding content.
5.**Popular Stores** and **Best Credit Cards** headings are visible, but their associated content is not properly rendered.
6.The page appears visually broken/incomplete.

**Expected Result**
All Home page sections should render completely and correctly.

For example:
Flash Sale
 ├── Countdown
 ├── Product cards
 └── View All

Thundering Deal
 ├── Deal content
 └── Product cards

Popular Stores
 └── Store cards

Best Credit Cards
 └── Credit card content/cards

**There should be:**
1.No unexpected blank spaces.
2.No cut-off sections.
3.No orphaned/empty UI elements.
4.No unexplained red horizontal bar.
5.Proper spacing between sections.
6.Complete rendering of section content.
7.Consistent layout throughout the Home page.

**Priority**
**High**

**Labels***
bug
ui
frontend
home-page
layout
content-rendering
responsive-ui
high-priority

**Environment**
**Field	                                        Details**
Application	                                   DealWallet
Page	                                       Home
Environment	                                   QA
Browser	                                       Google Chrome
OS	                                           Windows
Device	                                       Desktop
View	                                       Desktop
Feature	                                       Home Page Sections

**Impact**
**High – UI/UX Impact**

This issue affects the overall Home page because users cannot properly view or interact with content in multiple sections.

**It may result in:**
1.Missing deals/content
2.Poor user experience
3.Users being unable to access products/stores/cards
4.Large unused areas on the page
5.Broken/incomplete appearance of the Home page

**Evidence**
Attached screenshot shows the issue:
1.Flash Sale section visible
2.Thundering Deal heading visible but content missing
3.Large red horizontal element
4.Popular Stores heading without visible content
5.Best Credit Cards heading without visible content
6.Large empty spaces between sections