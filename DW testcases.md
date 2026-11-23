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

**Testcase 5**
**Title**:“View All” Redirects to Store Page but Displays “Something Went Wrong” After Loading

**Description**
1.When the user clicks the “View All” button from the Home page, the application redirects to the expected store/listing URL. However, after a few seconds, the destination page fails to load correctly and displays:
          **Something went wrong!**
2.Please try again. If it keeps happening, refresh the page.
3.The issue occurs even though the user's internet connection is working normally.

**Preconditions**
1.User can access the DealWallet Home page.
2.Home page is loaded successfully.
3.The View All button is available.
4.Internet connection is active.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Navigate to the relevant section containing the View All button.
3.Click View All.
4.Verify that the browser redirects to the store/listing page.
5.Wait for a few seconds.
6.Observe the destination page.

**Actual Result**
1.The View All button redirects the user to a store/listing URL.
2.After a few seconds, the destination page displays:
      **“Something went wrong!”**
3.“Please try again. If it keeps happening, refresh the page.”
4.The expected store/product listing content is not displayed.

**Expected Result**
**After clicking View All:**
1.User should be redirected to the correct listing/store page.
2.The destination page should load successfully.
3.Relevant stores/products should be displayed.
4.The page should not show a generic error when valid data is available.
5.If the backend/API fails, the application should display an appropriate user-friendly error and log the technical failure for debugging.

**Internet Connectivity Evidence**
**The internet speed test performed during testing shows approximately:**
**Metric**                         	**Result**
Download	                            67.07 Mbps
Upload	                            14.48 Mbps
Ping	                               19 ms
**This indicates that the test environment had an active internet connection with reasonable latency and bandwidth at the time of testing.**

Therefore, the issue should **not be immediately classified as an internet connectivity problem.** The frontend/API/backend request should be investigated.

**Priority**
**High**

**Labels**
bug
qa
frontend
backend
api
home-page
view-all
store-page
navigation
high-priority    

**Environment**
**Field**   	                           **Details**
Application	                               DealWallet
Module	                                  Home Page → View All
Browser	                                  Google Chrome
OS	                                        Windows
Environment	                               QA
Device	                                  Desktop
Connection	                               Internet connected
Download Speed	                            67.07 Mbps
Upload Speed	                            14.48 Mbps
Ping	                                     19 ms

**Impact**
**High – Functional Impact**
Users are unable to access the content through the **View All** navigation.

This can result in:
1.Users being redirected to a page that fails to load.
2.Store/product listings becoming inaccessible.
3.Loss of navigation flow from the Home page.
4.Poor user experience.
5.Potential loss of engagement when users try to explore additional deals/stores.

**Evidence**
**Screenshot 1:** Destination page showing:
    **Something went wrong!**

after clicking **View All.**

**Screenshot 2:** Internet speed test showing:
1.Download: **67.07 Mbps**
2.Upload: **14.48 Mbps**
3.Ping: **19 ms**
The second screenshot can be attached as supporting evidence that the failure occurred while the internet connection was active.

**Testcase 6**
**Title**:Product Search Returns “No Data Found” for Existing Products

**Description**
1.The product search functionality is not returning results for products that are already available on the Home page.
2.When searching for **“t shirts”**, the search component displays **“No data found.”** However, multiple T-shirt products are visible in the Home page product listings.
3.This indicates that the search functionality may not be correctly matching the entered keyword against the available product names/data.

**Preconditions**
1.DealWallet Home page is accessible.
2.Product data is available.
3.T-shirt products are present in the product listings.
4.Search functionality is enabled.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Locate the search bar.
3.Enter:
     **t shirts**
4.Observe the search suggestions/results popup.
5.Verify that it displays:
    **“No data found.”**
6.Close the search popup.
7.Browse the Home page product listings.
8.Observe that multiple T-shirt products are available.

**Actual Result**
The search returns:
          **No data found.**
However, T-shirt products are available on the Home page.
Examples visible in the screenshot:
1.Men's T-Shirt
2.Men's Running T-Shirt
3.Men's Cotton Blend Polo T-Shirt
4.Men's Cotton Regular Fit Half Sleeves Crew Neck T-Shirt
5.Athleisure Men's Polo T-Shirt

**Expected Result**
When the user searches for:
    **t shirts**
the search functionality should return relevant products whose names or searchable fields match the keyword.

For example:
 Search: t shirts

Results:
✓ Men's T-Shirt
✓ Men's Running T-Shirt
✓ Men's Cotton Blend Polo T-Shirt
✓ Athleisure Men's Polo T-Shirt
...
The search should not display **“No data found”** when matching products are available.

**Priority**
**High**

**Labels**
bug
qa
search
product-search
frontend
backend
api
high-priority

**Environment**
**Field**   	                                 **Details**
Application	                                    DealWallet
Page	                                          Home
Feature	                                       Product Search
Browser	                                       Google Chrome
OS	                                             Windows
Environment	                                    QA
Search Keyword	                                 t shirts
Device	                                       Desktop

**Impact**
**High – Functional Impact**
Users may be unable to discover products through search even though those products are available in the application.
This can cause:
1.Incorrect “No data found” messages.
2.Users missing available products.
3.Reduced product discoverability.
4.Search functionality becoming unreliable.
5.Poor user experience.

**Evidence**
**Screenshot 1:** Searching for t shirts displays:
      **No data found.**

**Testcase 7**
**Title**:Redesign Blog Page with Professional Dark and Light Mode UI

**Description**
1.Redesign the existing DealWallet Blog page to provide a more professional, modern, and consistent blog experience.
2.The current Blog page has a basic layout with a large empty content area, simple search/filter controls, and blog cards with limited information.
**The new design should introduce a structured Blog experience with:**
1.Professional Blog hero section
2.Improved Blog heading and description
3.Blog search
5.Category filters
6.Sort By functionality
7.Grid/List view option
8.Improved blog cards
9.Blog category badges
10.Blog metadata
11.Reading time
12.Read More CTA
13.Favorite/save icon
14.Pagination
15.Consistent Dark Mode
16.Matching Light Mode
17.Responsive layout
The **same structure and functionality should be maintained between Dark and Light modes,** with only the theme styling changing.

**Old vs New Comparison**
**Feature	                    Current / Old	                                      New / Proposed**
Blog Header	                  Basic DealWallet Blogs heading	                 Professional DealWallet Blog hero section
Header Description	          Simple description	                             Clear Blog tagline and supporting text
Hero Section	              ❌ No dedicated hero design                       ✅ Dedicated Blog hero banner
Search	                      Basic search box	                                 Prominent article/search bar
Search Placeholder	          Search electronics blogs...	                     Search articles, guides & shopping tips...
Search CTA	                  Search icon	                                     Search button + icon
Categories	                  Basic dropdown	                                 Category chips/buttons
Categories Available	      All Categories	                                 All Categories, Electronics, Buying            Guide,Tips & Tricks, Reviews, News
Sort	                      Basic dropdown	                                 Improved Sort By control
View Mode	                  ❌ Not available	                               ✅ Grid/List view
Blog Count	                  Showing 10 Blog(s)	                             Retained and visually improved
Blog Cards	                  Basic cards	                                     Professional structured cards
Blog Image	                  Basic/placeholder                                  appearance	Large visual blog image
Category	                  ❌ Limited/not clearly displayed	               ✅ Category badge
Blog Title	                  Basic	                                             Strong visual hierarchy
Description	                  Limited	                                         Short article summary
Date	                      ❌ Not clearly shown	                           ✅ Publication date
Reading Time	              ❌ Not shown	                                   ✅ Reading time
Favorite	                  Heart icon	                                     Save/favorite icon maintained and styled
CTA	                          ❌ Limited	                                       ✅ Read More →
Pagination	                  ❌ Not clearly available	                       ✅ Pagination
Dark Mode	                  Existing dark theme	                             Redesigned professional dark theme
Light Mode	                  Not properly represented	                         ✅ Dedicated light theme
Responsive UI	              Needs validation	                                 Must support desktop/tablet/mobile
Visual Consistency	          Basic	                                             Consistent professional design system

**Preconditions**
1.DealWallet application is accessible.
2.User can access the Blog page.
3.Blog data is available.
4.Dark mode and light mode are available in the application or theme support is implemented.
5.Existing blog functionality should continue working after redesign.

**Proposed New Layout**
**Dark Mode**
┌─────────────────────────────────────────────────────────────┐
│ DealWallet    Home Deals Stores Coupons Blog Forum   Login │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│              BLOG                                           │
│              DealWallet Blog                                │
│              Your guide to smarter shopping, latest trends  │
│              and insights in electronics.                   │
│                                                             │
│   🔍 Search articles, guides & shopping tips     Search    │
│                                                             │
└─────────────────────────────────────────────────────────────┘

[All Categories] [Electronics] [Buying Guide]
[Tips & Tricks] [Reviews] [News]

Showing 10 Blogs                         Sort By: Latest
                                         Grid | List

Latest Blogs

┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
│   Image    │ │   Image    │ │   Image    │ │   Image    │
│ Electronics│ │Buying Guide│ │  Reviews   │ │Tips & Tricks│
│            │ │            │ │            │ │            │
│ Blog Title │ │ Blog Title │ │ Blog Title │ │ Blog Title │
│ Description│ │ Description│ │ Description│ │ Description│
│ Date · 5m  │ │ Date · 6m  │ │ Date · 4m  │ │ Date · 5m  │
│ Read More →│ │ Read More →│ │ Read More →│ │ Read More →│
└────────────┘ └────────────┘ └────────────┘ └────────────┘

                    ← 1 2 3 ... 5 →

**Light Mode**
**The same layout should be maintained, but with:**
1.White/light background
2.Dark text
3.Light cards
4.Subtle borders/shadows
5.Blue primary CTA
6.Light category badges
7.Proper contrast
The **layout should not change between Dark and Light mode.**

Only the visual theme should change.

**Steps to Implement / Verify**
**Step 1 — Open Blog page**
Navigate to:
      **DealWallet → Blog***

**Step 2 — Verify Blog Hero**
Verify:
1.Blog label
2.Blog title
3.Description
4.Hero background
5.Search field
6.Search button

**Step 3 — Verify Search**
Search using a valid keyword.
Example:
                **electronics**
Verify relevant blogs are displayed.

**Step 4 — Verify Categories**
Check:
1.All Categories
2.Electronics
3.Buying Guide
4.Tips & Tricks
5.Reviews
6.News
Verify selecting a category filters the blog results correctly.

**Step 5 — Verify Sorting**
Verify:
     **Latest**
and any other supported sorting options.

**Step 6 — Verify View Mode**
Test:
    **Grid View**
    **List View**
Verify that both layouts display blog information correctly.

**Step 7 — Verify Blog Card**
Each card should contain:
1.Image
2.Category
3.Title
4.Description
5.Date
6.Reading time
7.Favorite/save
8.Read More

**Step 8 — Verify Pagination**
Verify:
Previous
1
2
3
...
5
Next
Pagination should correctly load the corresponding blogs.

**Step 9 — Verify Dark Mode**
Check:
1.Background
2.Text
3.Cards
4.Borders
5.Buttons
6.Category badges
7.Icons
8.Search
9.Pagination

**Step 10 — Verify Light Mode**
Switch to Light Mode and verify the same components.

**Step 11 — Responsive Testing**
Test:
1.Desktop
2.Tablet
3.Mobile
No text, cards, buttons, images, or controls should be cut off.

**Expected Result**
1.The Blog page should have a **consistent professional design in both Dark and Light modes.**
2.All existing Blog functionality should continue working:
a.Search
b.Category filtering
c.Sorting
d.Blog navigation
e.Favorite/save
f.Read More
g.Pagination
3.The redesign should improve the visual hierarchy without breaking existing functionality.

**Priority**
**Medium**
This is a UI/UX feature improvement rather than a blocking functional issue.

**Labels**
  **rren**

**Environment**
**Field	                                  Details**
Application	                             DealWallet
Module	                                 Blog
Environment	                             QA
Browser	                                 Google Chrome
OS	                                     Windows
Device	                                 Desktop
Theme 1	                                 Dark Mode
Theme 2	                                 Light Mode
Responsive	                             Desktop / Tablet / Mobile

**Impact**
**Current**
The existing Blog page has:
1.Excessive empty space
2.Basic visual hierarchy
3.Limited blog metadata
4.Basic filtering UI
5.Limited navigation controls
6.Less consistent card presentation

**After redesign**
The new design provides:
1.Better content discovery
2.Clearer Blog navigation
3.Better article information
4.Improved search/filter experience
5.Better visual consistency
6.Consistent Dark/Light mode
7.More professional presentation
8.Better responsive experience

**QA Acceptance Criteria**
**Blog Header**
1.Blog hero section is displayed.
2.DealWallet Blog title is displayed.
3.Supporting description is displayed.
4.Hero design is consistent with DealWallet branding.

**Search**
1.Search field is visible.
2.Search icon is visible.
3.Search button is visible.
4.Search returns relevant blogs.
5.Empty search result is handled correctly.

**Categories**
1.All Categories works.
2.Electronics works.
3.Buying Guide works.
4.Tips & Tricks works.
5.Reviews works.
6.News works.

**Sorting**
1.Sort By is available.
2.Latest sorting works.
3.Additional supported sorting options work.

**Blog Cards**
1..Blog image displays correctly.
2.Category badge displays correctly.
3.Title displays correctly.
4.Description displays correctly.
5.Date displays correctly.
6.Reading time displays correctly.
7.Favorite icon works.
8.Read More works.

**View**
1.Grid view works.
2.List view works.
3.Switching views does not lose filters/search state unless specified.

**Pagination**
1.Page numbers work.
2.Previous works.
3.Next works.
4.Correct blogs load for each page.

**Dark Mode**
1.No text visibility issues.
2.No contrast issues.
3.Cards are properly styled.
4.Buttons are visible.
5.Icons are visible.
6.Search is readable.
7.Pagination is readable.

**Light Mode**
1.No text visibility issues.
2.Cards are properly styled.
3.Borders/shadows are visible.
4.Buttons are readable.
5.Icons are visible.
6.Search is readable.
7.Pagination is readable.

**Responsive**
1.Desktop layout works.
2.Tablet layout works.
3.Mobile layout works.
4.No horizontal overflow.
5.No content is cut off.
6.No overlapping elements.
7.Blog cards resize correctly.

**Testcase 8**
**Title**:Add Food Category Products to the Thundering Deal Section

**Description**
1.The Food category is currently displayed under the **Thundering Deal** section on the DealWallet Home page, but there are no Food-related products available under this category.
2.Food-related products need to be added and correctly mapped to the **Food** category so that selecting the Food category displays relevant products.

**Preconditions**
1.DealWallet Home page is accessible.
2.Thundering Deal section is available.
3.Food category is configured and displayed.
4.Product management/admin access is available to add products.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the **Thundering Deal** section.
3.Select the **Food** category.
4.Observe the product listing.

**Actual Result**
The **Food** category is displayed, but there are currently **no Food products** available under it.

**Expected Result**
Food-related products should be added to the product catalog and mapped to the **Food** category.

After the products are added:
1.Click Food.
2.Food-related products should be displayed.
3.Each product should have valid:
    1.Product image
    2.Product name
    3.Category
    4.Price
    5.Discount, if applicable
    6.Rating, if applicable
    7.Buy Now/CTA
Products should appear correctly within the **Thundering Deal** section.

**Example Food Products**
Products could include categories such as:
1.Snacks
2.Biscuits
3.Chocolates
4.Dry Fruits
5.Cooking Essentials
6.Beverages
7.Packaged Foods
8.Instant Foods

**Priority**
**Medium**

**Labels**
feature
product-data
food
category
thundering-deal
home-page
qa

**Environment**
**Field	                                                 Details**
Application	                                            DealWallet
Module	                                                Home Page
Section	                                                Thundering Deal
Category	                                            Food
Environment	                                            QA
Browser	                                                Google Chrome
OS	                                                    Windows
Device	                                                Desktop

**Impact**
Currently, the **Food** category provides no products to users.
Adding products will ensure that:
  1.Food category has meaningful content.
  2.Users can browse Food deals.
  3.Category selection works as expected.
  4.Thundering Deal has complete category coverage.
  5.The Home page provides a consistent experience across categories.

**Acceptance Criteria**
1.Food products are added to the product catalog.
2.Products are correctly mapped to the **Food** category.
3.Food products appear when the Food category is selected.
4.Product images load correctly.
5.Product names are displayed correctly.
6.Prices are displayed correctly.
7.Discounts display correctly where applicable.
8.Product cards follow the existing DealWallet design.
9.Buy Now functionality works.
10.Food products do not appear under unrelated categories.
11.Existing categories continue to work without regression.

**Testcase 9**
**Title**:Fashion & Lifestyle Category Is Missing Description in Shop by Category Section

**Description**
1.In the **Shop by Category** section on the DealWallet Home page, category cards display a short description below the category name.
2.However, the **Fashion & Lifestyle category** does not have a description, while other categories such as **Beauty, Home Appliances, Makeup, and Bags** display descriptions.
3.This results in an inconsistent presentation across the category cards.

**Preconditions**
1.DealWallet Home page is accessible.
2.**Shop by Category** section is available.
3.Category cards are loaded.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the **Shop by Category** section.
3.Observe the category cards.
4.Compare the **Fashion & Lifestyle** card with other category cards such as:
      1.Beauty
      2.Home Appliances
      3.Makeup
      4.Bags
5.Observe the content displayed below each category name.

**Actual Result**
The **Fashion & Lifestyle** category displays:
   1.Category image 
   2.Category name
   3.Deal count
But the category description is missing.

Other category cards contain descriptions, for example:
**Beauty**
**Skincare, haircare, and personal grooming products...**

**Home Appliances**
**Electrical devices like ACs, fridges, and washing machines...**

**Expected Result**
The Fashion & Lifestyle category should also contain a relevant category description consistent with the other category cards.

Example:

**Fashion & Lifestyle**
**Fashion, clothing, accessories, footwear, and lifestyle products for everyday style...**

The description should follow the same:
1.Font style
2.Font size
3.Color
4.Spacing
5.Maximum text length
6.Position
as the descriptions used for the other category cards.

**Priority**
**Medium**

**Labels**
bug
qa
ui
home-page
shop-by-category
content
category
frontend

**Environment**
**Field	                                Details**
Application	                            DealWallet
Page	                                Home
Section	                                Shop by Category
Category	                            Fashion & Lifestyle
Environment	                            QA
Browser	                                Google Chrome
OS	                                    Windows
Device	                                Desktop

**Impact**
**Low–Medium – UI Consistency Impact**

The issue does not prevent users from accessing the category, but it causes:
 1.Inconsistent category card presentation.
 2.Uneven information hierarchy.
 3.Reduced visual consistency.
 4.Fashion & Lifestyle card appears different from the other category cards.

**Evidence**
The screenshot shows the **Shop by Category** section.
1.**Fashion & Lifestyle:** Description is missing.
2.**Other categories:** Description is displayed.

**Testcase 10**
**Title**:Ajio Store Card Is Missing Category Label in Top Weekly Deals

**Description**
1.In the **Top Weekly Deals** section on the DealWallet Home page, the Ajio store card does not display its category label.
2.Other store cards in the same section display their respective category labels, resulting in an inconsistent presentation of store information.

**Preconditions**
1.DealWallet Home page is accessible.
2.Top Weekly Deals section is available.
3.Ajio store is displayed in the Top Weekly Deals section.
4.Other store cards with category information are available.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the **Top Weekly Deals** section.
3.Locate the **Ajio** store card.
4.Compare the Ajio card with the other store cards.
5.Observe the category information below each store name.

**Actual Result**
The **Ajio** card displays:
1.Ajio logo
2.Ajio store name
3.Deals count
4.Coupons count
5.Shop button
However, the **category label** is missing.

Other stores display category information, for example:
Croma
Electronics & Technology

Snapdeal
Baby & Kids

ZOP
Baby & Kids

Flipkart
E-commerce Marketplace

**Expected Result**
1.The Ajio store card should display its appropriate category label below the store name, consistent with the other Top Weekly Deals cards.
2.For example:
**Ajio**
**Fashion & Lifestyle**
3.The exact category should be based on the category configured for Ajio in the application data.

**Priority**
**Medium**

**Labels**
bug
qa
ui
home-page
top-weekly-deals
store
category
data-consistency

**Environment**
**Field	                             Details**
Application	                         DealWallet
Page	                             Home
Section	                             Top Weekly Deals
Store	                             Ajio
Environment	                         QA
Browser	                             Google Chrome
OS	                                 Windows
Device	                             Desktop

**Impact**
**Medium – UI/Data Consistency**
The issue does not prevent users from opening or shopping from Ajio, but it creates an inconsistent store-card layout and results in incomplete store information.

**Evidence**
The attached screenshot shows:
1.**Ajio:** category label missing.
2.**Croma:** Electronics & Technology displayed.
3.**Snapdeal:** Baby & Kids displayed.
4.**ZOP:** Baby & Kids displayed.
5.**Flipkart:** E-commerce Marketplace displayed.

**Testcase 11**
**Title**:Share Popup Overlaps Store Card Content on Stores Page

**Description**
1.On the DealWallet Stores page, clicking the Share icon on a store card opens the share popup in an incorrect position. The popup overlaps the store card content and is partially clipped by the card/container.
2.The share popup should be positioned clearly without covering or being clipped by the store card content.

**Preconditions**
1.DealWallet Stores page is accessible.
2.Store cards are displayed.
3.Share icon is available on the store card.

**Steps to Reproduce**
1.Open the DealWallet Stores page.
2.Locate any store card.
3.Click the Share icon.
4.Observe the share popup.
5.Check its position relative to the store card and surrounding content.

**Actual Result**
1.Share popup overlaps the store card.
2.Share content is partially clipped.
3.The popup appears within the card/container instead of being displayed cleanly.
4.Some share options are difficult to view or interact with.

**Expected Result**
The share popup should:
1.Open in a clearly visible position.
2.Not overlap important store-card content unnecessarily.
3.Not be clipped by the card/container.
4.Display all available share options completely.
5.Remain within the viewport.
6.Automatically reposition when there is insufficient space.

**Priority**
**Medium**

**Labels**
bug
qa
ui
ux
stores
share
popup
responsive-ui
frontend

**Environment**
**Field	                                  Details**
Application	                              DealWallet
Page	                                  Stores
Feature	                                  Store Share
Environment	                              QA
Browser	                                  Google Chrome
OS	                                      Windows
Device	                                  Desktop
Theme	                                  Dark Mode

**Impact**
**Medium – UI/UX Impact**
Users may have difficulty accessing the share options because the popup is partially hidden and overlaps the store card.

**Evidence**
Attached screenshot showing the share popup overlapping the **Meesho** store card.

**Likely Owner**
**Frontend/UI team**
1.The issue is most likely related to popup positioning, CSS overflow, z-index, or the popup's positioning logic.
2.Developers should check:
       position
       z-index
       overflow
       top / bottom / left / right
       viewport boundaries

**QA Acceptance Criteria**
1.Share popup opens correctly.
2.Popup does not get clipped.
3.All share options are visible.
4.Popup does not incorrectly cover store-card content.
5.Popup stays within the browser viewport.
6.Popup repositions when near the screen edge.
7.Share functionality works correctly.
8.Same behavior works for other store cards.
9.Desktop and responsive layouts are verified.

**Testcase 12**
**Title**:Ajio Store Redirects to Invalid Cuelinks URL and Displays Not Found Error

**Description**
1.When the user clicks the Ajio store from the Top Weekly Deals section on the DealWallet Home page, the application redirects to an incorrect Cuelinks URL.
2.Instead of navigating to the intended Ajio store/affiliate destination, the browser opens:
        **dealwallet.com/www.cuelinks.com**
3.The destination page then displays a Not Found error.

**Preconditions**
1.DealWallet Home page is accessible.
2.Top Weekly Deals section is displayed.
3.Ajio store is available in the section.
4.Ajio store has a configured store/affiliate URL.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the Top Weekly Deals section.
3.Locate the Ajio store card.
4.Click the Ajio store/card or its Shop action.
5.Observe the URL after redirection.
6.Observe the destination page.

**Actual Result**
1.The user is redirected to an invalid URL similar to:
      **https://dealwallet.com/www.cuelinks.com**
2.The page displays:
   **Not Found**
       **Could not find requested resource**
3.The Ajio store page is not opened.

**Expected Result**
1.Clicking the Ajio store should redirect the user to the **correct configured Ajio store/affiliate URL.**
2.The URL should be handled as a valid external URL rather than being appended as a relative path to dealwallet.com.
3.The destination should load successfully without a **Not Found** error.

**Priority**
**High**

**Labels**
bug
qa
high-priority
navigation
redirect
affiliate-link
store
ajio
cuelinks
home-page
top-weekly-deals

**Environment**
**Field	                    Details**
Application	                DealWallet
Page	                    Home
Section	                    Top Weekly Deals
Store	                    Ajio
Environment	                QA
Browser	                    Google Chrome
OS	                        Windows
Device	                    Desktop
Theme	                    Dark Mode

**Impact**
**High – Functional Impact**
1.Users cannot access the Ajio store through the Top Weekly Deals section.
2.This can result in:
     1.Broken store navigation.
     2.Users seeing a Not Found page.
     3.Ajio deals becoming inaccessible.
     4.Affiliate/store tracking potentially not working as intended.
     5.Loss of the intended shopping flow.

**Testcase 13**
**Title**:Standardize Button Colors Across Home Page

**Description**
1.On the DealWallet Home page, different sections are using different colors for primary action buttons.
2.For example:
   1.Buy Now buttons on product cards use one blue shade.
   2.Shop buttons in the Top Weekly Deals section use another blue shade.
3.This creates an inconsistent visual theme across the Home page.
4.All primary action buttons should follow a single standardized button color/theme throughout the application.

**Preconditions**
1.DealWallet Home page is accessible.
2.Product cards are displayed.
3.Top Weekly Deals section is displayed.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to a product listing section.
3.Observe the Buy Now button on a product card.
4.Scroll to the Top Weekly Deals section.
5.Observe the Shop button on the store cards.
6.Compare the button colors.

**Actual Result**
1.Different primary action buttons use different blue shades/styles.
**Product card:**
          **Buy Now → darker blue**
**Top Weekly Deals:**
          **Shop → brighter blue**
2.This makes the CTA styling inconsistent across the Home page.

**Expected Result**
1.All primary CTA buttons should use the same standardized theme color.
2.For example:
  Primary CTA

┌─────────────────────┐
│      Buy Now        │
└─────────────────────┘

┌─────────────────────┐
│       Shop          │
└─────────────────────┘
3.Both should have the same:
   1.Background color
   2.Hover color
   3.Text color
   4.Border radius
   5.Typography
   6.Shadow/elevation
   7.Disabled state, where applicable
4.Only the button text/icon should differ based on the action.

**Recommended Design**
1.Use the existing brighter DealWallet blue used by the Top Weekly Deals Shop button as the standard primary CTA color, provided it meets the application's contrast requirements.
2.Example:
**Primary Button**
       1.Blue background
       2.White text
       3.Rounded corners
       4.Consistent hover state
       5.Consistent focus state

**Priority**
**Medium**

**Labels**
bug
qa
ui
ux
design-system
button
home-page
frontend
consistency

**Environment**
**Field	                          Details**
Application	                      DealWallet
Page	                          Home
Environment	                      QA
Browser	                          Google Chrome
OS	                              Windows
Device	                          Desktop
Theme	                          Dark Mode

**Impact**
**Medium – UI Consistency**
1.Inconsistent CTA colors can:
        1.Reduce visual consistency.
        2.Make the application look less polished.
        3.Make different actions appear to have different importance.
        4.Create inconsistency in the overall design system.

**Testcase 14**
**Title**:Fix Back Button Overlapping Credit Card Landing Page Banner

**Description**
1.On the DealWallet Home page, when a user clicks a credit card from the Best Credit Cards section, they are redirected to the credit card landing/details page.
2.On the landing page, the ← Back button is positioned over the top-left area of the hero/banner section, causing it to overlap with the banner content.

**Steps to Reproduce**
1.Open the DealWallet Home page.
2.Scroll to the Best Credit Cards section.
3.Click any credit card.
4.Observe the credit card landing/details page.
5.Check the position of the ← Back button.

**Actual Result**
1.The ← Back button overlaps the credit card hero/banner section.
2.The button appears on top of the banner instead of having its own proper spacing/position.

**Expected Result**
1.The ← Back button should have a dedicated position above the hero banner with sufficient spacing.
2.**Recommended layout:**
← Back

┌───────────────────────────────────────────────┐
│                                               │
│          Credit Card Hero Banner              │
│                                               │
│   Unlock Premium Benefits       [Card Image]  │
│                                               │
└───────────────────────────────────────────────┘
3.The Back button should not overlap or cover any banner content.

**UI Requirements**
1.Move the Back button outside the hero/banner container.
2.Maintain consistent spacing between the Back button and banner.
3.Keep the Back button clearly visible in both Dark Mode and Light Mode.
4.Ensure the button remains properly positioned on different screen sizes.
5.Maintain the existing Back button functionality.
5.Ensure the hero banner content is not shifted, hidden, or covered.

**Acceptance Criteria**
1.Back button does not overlap the hero banner.
2.Back button appears above the banner with proper spacing.
3.Banner content is completely visible.
4.Layout works correctly on desktop.
5.Layout remains responsive on tablet/mobile.
6.Dark Mode is verified.
7.Light Mode is verified.
8.Back navigation functionality remains unchanged.
9.No regression on other credit card landing pages.

**Priority**
**Medium**

**Type / Labels**
bug qa ui ux responsive credit-cards frontend

**Evidence**
1.**Actual issue:**The ← Back button is visually overlapping the top-left portion of the credit card hero/banner on the landing page.
2.**Expected:**The Back button should be positioned separately above the banner with proper spacing.