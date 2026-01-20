### Activate CRM Application in odoo Apps page.

# What is Odoo CRM?
**Definition:** Odoo CRM (Customer Relationship Management) is a software application that helps businesses organize, track, and manage their sales activities, customer interactions, and sales pipeline.
**Purpose:**

* Track potential customers (leads) from first contact to final sale
* Organize sales opportunities in a visual pipeline
* Manage sales teams and their performance
* Forecast revenue and sales targets
* Prevent duplicate contacts and streamline communication


# Key Terms You Should Know

* **Lead:** A potential customer who has shown interest in your product/service
* **Opportunity:** A qualified lead that has a good chance of becoming a sale
* **Pipeline:** A visual representation of all your sales opportunities at different stages
* **Sales Team:** A group of salespeople working together with shared goals
* **Lost Opportunity:** A potential sale that didn't convert to an actual sale


# 1. Managing Lost Opportunities
## What are Lost Opportunities?
Lost opportunities are potential sales that didn't result in a successful deal. Tracking these helps you:

* Understand why deals fail
* Improve your sales strategy
* Identify training needs for your team
* Keep your pipeline accurate

### Step-by-Step: How to Mark an Opportunity as Lost

1. **Open the CRM app**
1. **Find the opportunity** you want to mark as lost in your pipeline
1. **Click on the opportunity card** to open its details
1. **Click the "Lost" button** at the top of the form
1. **Choose a reason** from the "Lost Reason" dropdown menu

 > * If you don't see a suitable reason, type a new one and click "Create"


6. **Add notes** in the "Closing Note" field (optional but recommended)
7. **Click "Mark as Lost"**

**Result:** A red "Lost" banner appears on the opportunity.
### Sample Lost Reasons to Try:

* "Competitor had better pricing"
* "Customer decided not to purchase"
* "Budget constraints"
* "Timeline didn't match customer needs"
* "Lost contact with prospect"

### Step-by-Step: How to View Lost Opportunities

1. **Go to CRM app → Sales → My Pipeline**
1. **Click the search bar** at the top
1. **Remove all default filters** (clear the search bar)
1. **Click the dropdown arrow** next to the search bar
1. **Select "Lost"** from the Filters section
1. **View all lost opportunities** that appear

### Step-by-Step: How to Restore a Lost Opportunity

1. **Filter to show lost opportunities** (follow steps above)
1. **Click on the lost opportunity** you want to restore
1. **Click "Restore"** button in the upper-left corner
1. **The red "Lost" banner disappears** - opportunity is now active again


# 2. Managing Similar Leads and Opportunities
## What are Similar Leads/Opportunities?
These are duplicate or nearly identical records in your system, usually created when:

* The same customer contacts you through different channels
* Multiple salespeople enter the same prospect
* A customer uses slightly different contact information

### How Odoo Identifies Similar Records
Odoo compares:

* Email addresses
* Phone numbers
* Contact names

When similarities are found, a "Similar Leads" button appears on the record.
### Step-by-Step: How to Merge Similar Records

1. **Open a lead or opportunity** that shows a "Similar Leads" button
1. **Click the "Similar Leads" button** to see all similar records
1. **Review each record** to confirm they should be merged
1. **Click the list view icon** to switch to list view
1. **Check the boxes** next to records you want to merge
1. **Click "Actions"** at the top of the page
1. **Select "Merge"** from the dropdown menu
1. **Choose a salesperson and sales team** for the merged record
1. **Click "Merge"** to complete the process

**Important:** Merging cannot be undone, so double-check before proceeding!
### When NOT to Merge Records

* **Different contacts** at the same company (they may have different needs)
* **Lost vs. active opportunities** (unless you want to reactivate the lost one)
* **Similar but not identical** email addresses (could be different people)
* **Multiple salespeople** are actively working on separate opportunities

### Sample Scenario:
**Merge These:**

* Lead 1: [john.smith@company.com](mailto:john.smith@company.com), Phone: 555-1234
* Lead 2: [john.smith@company.com](mailto:john.smith@company.com), Phone: 555-1234
* (Same person, same contact info)

**Don't Merge These:**

* Lead 1: [john.smith@company.com](mailto:john.smith@company.com)
* Lead 2: [mary.jones@company.com](mailto:mary.jones@company.com)
* (Different people at same company)


# 3. Managing Sales Teams
## What is a Sales Team?
A sales team is a group of salespeople who work together with:

* Shared sales targets
* Common assignment rules
* Team leader supervision
* Coordinated sales activities

### Step-by-Step: How to Create a Sales Team

1. **Go to CRM app → Configuration → Sales Teams**
1. **Click "New"**
1. **Enter a team name** in the "Sales Team" field
1. **Select a Team Leader** from the dropdown
1. **Set an Email Alias** (optional) - creates leads automatically when emails are sent to this address
1. **Choose email acceptance level:**

* > Everyone: Any email creates a lead
* > Authenticated Partners: Only known contacts
* > Followers Only: Only team members
* > Authenticated Employees: Only company employees


7. **Select a Company** (if you have multiple companies)
8. **Click "Save"**

### Step-by-Step: How to Add Team Members

1. **Open the sales team** you want to edit
1. **Click the "Members" tab**
1. **Click "Add"**
1. **Select a salesperson** from the dropdown
1. **Set lead limits** in "Leads (30 days)" field
1. **Check "Skip auto assignment" **if you don't want automatic lead assignment
1. **Click "Save & Close"** or "Save & New" for more members

### Sample Sales Team Structure:
**Team Name:** Enterprise Sales Team
**Team Leader:** Sarah Johnson
**Members:**

* Mike Chen (Max 20 leads/month)
* Lisa Rodriguez (Max 15 leads/month)
* David Park (Max 25 leads/month)

### Step-by-Step: How to View Team Dashboard

1. **Go to CRM app → Sales → Teams**
1. **View your team's performance card** showing:

* > Open opportunities
* > Quotations sent
* > Sales orders
* > Expected revenue
* > New opportunities graph
* > Invoicing progress


3. **Click "Pipeline"** to view team's opportunities
4. **Click the three dots** in corner for team settings

***
## Practice Exercises
### Exercise 1: Lost Opportunity Management

1. Create a test opportunity called "ABC Corp - Software License"
1. Mark it as lost with reason "Budget constraints"
1. Add a closing note: "Customer will reconsider in Q2 next year"
1. Filter to view all lost opportunities
1. Restore the opportunity back to active status

### Exercise 2: Managing Similar Records

1. Create two leads with similar information:

> * Lead 1: "John Smith" at [john.smith@techcorp.com](mailto:john.smith@techcorp.com)
> * Lead 2: "J. Smith" at [john.smith@techcorp.com](mailto:john.smith@techcorp.com)


2. Notice the "Similar Leads" button appears
3. Compare the records and merge them
4. Verify the merged record contains information from both original leads

### Exercise 3: Sales Team Setup

1. Create a new sales team called "Regional Sales West"
1. Add yourself as team leader
1. Set up an email alias: [west-sales@yourcompany.com](mailto:west-sales@yourcompany.com)
1. Add 2-3 team members with different lead limits
1. View the team dashboard and explore the pipeline

# Acquire Leads
# 4. Lead Generation and Management
## What are Leads?
**Definition:** A lead is a potential customer who has shown initial interest in your product or service but hasn't been fully qualified yet.
**Purpose:**

* Capture potential customer information early
* Qualify prospects before assigning to salespeople
* Track the source of new business opportunities
* Organize and prioritize follow-up activities

### Key Differences: Leads vs Opportunities

* **Lead:** Early stage, not yet qualified, needs investigation
* **Opportunity:** Qualified prospect with real potential to buy

### Step-by-Step: How to Enable Leads Feature

1. **Go to CRM app → Configuration → Settings**
1. **Check the "Leads" checkbox**
1. **Click "Save"**
1. **Notice the new "Leads" menu** appears in the header

**Result:** Your CRM now captures leads before converting them to opportunities.
## Method 1: Creating Leads from Website Contact Forms
### Step-by-Step: Set Up Contact Form for Lead Generation

1. **Go to Website app → Contact Us**
1. **Click "Edit"** in the top-right corner
1. **Click on the contact form** to open settings
1. **In the "Action" dropdown,** select "Create an Opportunity"
1. **Choose a Sales Team** from the dropdown
1. **Select a Salesperson** (optional - can use team rules)
1. **Set "On Success"** behavior:

> * **Nothing:** Shows confirmation message
> * **Redirect:** Sends to thank-you page
> * **Show Message:** Displays custom message


8. **Click "Save"**

### Sample Contact Form Configuration:

* **Action:** Create an Opportunity
* **Sales Team:** "Web Inquiries Team"
* **Salesperson:** Auto-assign based on rules
* **On Success:** Redirect to "Thank You" page

### Step-by-Step: Customize Form Fields

1. **Click on any form field** while in edit mode
1. **Configure field settings:**

* **Type:** Text, Email, Phone, URL
* **Label:** Field name (e.g., "Company Size")
* **Required:** Toggle on/off
* **Placeholder:** Example text (e.g., "[john@company.com](mailto:john@company.com)")
* **Description:** Helper text for users


3. **Set visibility** for desktop/mobile
4. **Save changes**

## Method 2: Creating Leads from Email
### Step-by-Step: Set Up Email Aliases for Lead Generation

1. **Go to CRM app → Configuration → Sales Teams**
1. **Click on a sales team** to open its settings
1. **In "Email Alias" field,** enter your desired email address

> * Example: "[sales@yourcompany.com](mailto:sales@yourcompany.com)"


4. **Set "Accept Emails From":**

> * **Everyone:** Any email creates a lead
> * **Authenticated Partners:** Only known contacts
> * **Followers Only:** Only team members
> * **Authenticated Employees:** Only company staff


5. **Click "Save"**

**Result:** When someone emails [sales@yourcompany.com](mailto:sales@yourcompany.com), a lead is automatically created.
### Sample Email Alias Setup:

* **Email Alias:** "[info@westregion.com](mailto:info@westregion.com)"
* **Accept From:** Everyone
* **Sales Team:** Regional Sales West
* **Auto-assignment:** Based on team rules

## Method 3: Manual Lead Creation
### Step-by-Step: Create a Lead Manually

1. **Go to CRM app → Leads**
1. **Click "New"** in the top-left
1. **Fill out the lead form:**

> * **Title:** Brief description (e.g., "Software inquiry from ABC Corp")
> * **Contact Name:** Person's name
> * **Company Name:** Organization name
> * **Email:** Contact email
> * **Phone:** Contact number
> * **Source:** How you found them


4. **Add notes** about the lead
5. **Click "Save"**

## Method 4: Lead Mining (Advanced Feature)
### What is Lead Mining?
**Definition:** An automated feature that generates leads based on specific criteria like industry, company size, and location.
**Purpose:** Find potential customers who match your ideal customer profile.
### Step-by-Step: Enable and Use Lead Mining

1. **Go to CRM app → Configuration → Settings**
1. **Check "Lead Mining" checkbox**
1. **Click "Save"**
1. **Go to CRM app → Sales → My Pipeline**
1. **Click "Generate Leads" button**
1. **Configure search criteria:**

> * **Target:** Companies only OR Companies + Contacts
> * **Countries:** Select target countries
> * **Industries:** Choose relevant industries
> * **Company Size:** Set employee range (e.g., 50-200)
> * **Sales Team:** Assign to specific team
> * **Salesperson:** Assign to specific person


7. **Click "Generate Leads"**

**Note:** Lead mining uses credits - each lead costs 1 credit.
### Sample Lead Mining Configuration:

* **Target:** Companies and their Contacts
* **Countries:** United States, Canada
* **Industries:** Technology, Software
* **Company Size:** 100-500 employees
* **Sales Team:** Enterprise Sales
* **Role Filter:** Decision Makers, IT Directors

### Step-by-Step: Convert Leads to Opportunities

1. **Go to CRM app → Leads**
1. **Click on a lead** to open it
1. **Review the lead information** carefully
1. **Check for "Similar Leads" button** - merge if duplicates exist
1. **Click "Convert to Opportunity"**
1. **Choose conversion action:**

> * **Convert to opportunity:** Create new opportunity
> * **Merge with existing:** Combine with similar record


7. **Select Salesperson and Sales Team**
8. **Choose customer option:**

> * **Create new customer: **Use lead info to create customer
> * **Link to existing:** Connect to current customer
> * **Don't link:** No customer connection


9. **Click "Create Opportunity"**

**Result:** Lead becomes an opportunity in your sales pipeline.

# 5. Quotation Management
## What are Quotations?
**Definition:** A formal document that outlines the products/services you're offering to a customer, including prices and terms.
**Purpose:**

* Present professional pricing to prospects
* Document what you're offering
* Track customer responses
* Convert opportunities into sales

### Step-by-Step: Create a Quotation from an Opportunity

1. **Go to CRM app → Sales → My Pipeline**
1. **Click on an opportunity** to open it
1. **Review and update** opportunity information
1. **Click "New Quotation"** at the top-left
1. **Handle customer information:**

> * If customer exists: Quotation opens normally
> * If no customer: Choose to create new, link existing, or no link


6. **Fill out quotation header:**

> * **Customer:** Verify customer information
> * **Invoice Address:** Where to send invoice
> * **Delivery Address:** Where to ship products
> * **Expiration Date:** When quote expires
> * **Payment Terms:** How customer pays


7. **Click "Save"**

### Step-by-Step: Add Products to Quotation
### Method 1: Add Individual Products

1. **In the "Order Lines" tab,** click "Add a product"
1. **Type product name** to search catalog
1. **Select product** from dropdown
1. **Update quantity** if needed
1. **Verify pricing** and details
1. **Repeat** for additional products

### Method 2: Use Product Catalog

1. **Click "Catalog" button** on quotation
1. **Browse products** by category
1. **Click "Add" button** on product cards
1. **Set quantities** using +/- buttons
1. **Click "Back to Quotation"** when done

### Step-by-Step: Organize Quote with Sections

1. **Click "Add a section**" in Order Lines
1. **Type section name** (e.g., "Hardware", "Software", "Services")
1. **Drag products** into appropriate sections using drag icon
1. **Arrange sections** in logical order

## Sample Quotation Structure:
**Section 1: Software Licenses**

* CRM Software (5 licenses) - 00/month
* Email Marketing Tool (1 license) - 00/month

**Section 2: Implementation Services**

* Setup and Configuration - ,500
* Training (2 sessions) - ,000

**Section 3: Ongoing Support**

* Monthly Support Package - 00/month

### Step-by-Step: Send Quotation to Customer

1. **Click "Preview"** to see customer view
1. **Review quotation** carefully
1. **Click "Return to edit mode"** if changes needed
1. **Click "Send by Email"** when ready
1. **Review email template:**

> * Subject line
> * Email message
> * PDF attachment (automatic)


6. **Customize message** if needed
7. **Click "Send"**

**Result:** Customer receives professional quotation via email with PDF attachment.
### Step-by-Step: Track Quotation Status

1. **Return to opportunity** using breadcrumbs
1. **Check "Quotations" smart button** for count
1. **Click smart button** to view all quotations
1. **Monitor customer responses** in chatter
1. **Follow up** as needed

### Step-by-Step: Mark Opportunity Won or Lost
**If Customer Accepts (Won):**

1. **Open the opportunity**
1. **Click "Won" button** at top-left
1. **Green "Won" banner** appears
1. **Opportunity moves** to Won stage

**If Customer Declines (Lost):**

1. **Open the opportunity**
1. **Click "Lost" button** at top-left
1. **Select lost reason** from dropdown:

> * "Price too high"
> * "Competitor chosen"
> * "No budget"
> * "Timeline doesn't work"


4. **Add closing notes** with details
5. **Click "Mark as Lost"**
6. **Red "Lost" banner** appears


## Practice Exercises
### Exercise 1: Website Lead Generation

1. Set up a contact form that creates opportunities
1. Assign to "Web Sales" team
1. Test the form by submitting sample information
1. Check that lead/opportunity appears in CRM
1. Convert lead to opportunity if using leads feature

### Exercise 2: Email Lead Generation

1. Create email alias "[inquiries@yourcompany-test.com](mailto:inquiries@yourcompany-test.com)"
1. Set to accept emails from everyone
1. Send test email to the alias
1. Verify lead is created automatically
1. Review lead information and email in chatter

### Exercise 3: Manual Lead Creation and Conversion

1. Create manual lead: "Tech Startup - ABC Corp"
1. Add contact: "John Smith, CTO"
1. Add notes: "Interested in CRM solution for 20 users"
1. Convert to opportunity
1. Assign to appropriate salesperson

### Exercise 4: Complete Quotation Process

1. Create opportunity: "Office Furniture - XYZ Company"
1. Generate quotation from opportunity
1. Add products in organized sections:

> * Desks (5 units)
> * Chairs (5 units)
> * Accessories section


4. Set 30-day expiration
5. Preview and send quotation
6. Practice marking as won/lost

### Exercise 5: Lead Mining (if available)

1. Enable lead mining feature
1. Purchase test credits
1. Generate leads for your industry
1. Review generated leads
1. Convert best prospects to opportunities

# Assign and Track Leads
### What is Lead Assignment and Tracking?
**Lead Assignment** is the process of distributing potential customers (leads) to the right salespeople or teams based on specific criteria like probability of success, location, or team capacity.
**Lead Tracking** involves monitoring and analyzing lead performance, activities, and distribution to ensure no opportunities are missed and sales teams work efficiently.
### Why is This Important?

* **Prioritize High-Value Opportunities:** Focus on leads most likely to convert
* **Balance Workload:** Ensure fair distribution among sales team members
* **Prevent Lost Opportunities:** Track overdue activities and unattended leads
* **Improve Sales Performance:** Make data-driven decisions about lead assignment


## Automatic Lead Assignment with Predictive Scoring
### What is Predictive Lead Scoring?
Odoo uses machine learning to automatically calculate the probability of winning each lead based on historical data. The system uses the **Naive Bayes probability model** to analyze factors like:

* Sales team assigned
* Lead source (social media, email, etc.)
* Geographic location
* Contact quality (phone/email availability)
* Lead tags and language

### Step-by-Step Setup
### Step 1: Configure Predictive Lead Scoring Variables

1. Go to **CRM → Configuration → Settings**
1. Under **Predictive Lead Scoring**, click **Update Probabilities**
1. Select variables to consider:

> * **State:** Geographic state
> * **Country:** Geographic country
> * **Phone Quality:** Phone number availability
> * **Email Quality:** Email address availability
> * **Source:** Lead origin (search engine, social media)
> * **Language:** Spoken language
> * **Tags:** Custom tags


4. Set the start date for calculations
5. Click **Confirm**


> **Note:** Stage and Team variables are always active and cannot be disabled.

### Step 2: Enable Rule-Based Assignment

1. Go to **CRM → Configuration → Settings**
1. Activate **Rule-Based Assignment**
1. Choose assignment frequency:

> * **Manually:** Triggered by user
> * **Repeatedly:** Automatic (set interval)



### Step 3: Configure Assignment Rules by Team

1. Go to **CRM → Configuration → Sales Teams**
1. Select a sales team
1. Under **Assignment Rules**, click **Edit Domain**
1. Click **Add Filter** to create rules

**Example Rule:** Assign leads with 20% or higher success probability

* Field: **Probability**
* Operator: **≥** (greater than or equal to)
* Value: **20**

### Step 4: Configure Individual Team Member Rules

1. From the sales team page, click on a team member in the **Members** tab
1. Edit the **Domain** section with specific criteria
1. Save changes

**Sample Assignment Rules to Try**
**High-Priority Team (Senior Sales Reps)**
> Probability ≥ 50
> AND Country = "United States"
> AND Phone Quality is set
**Medium-Priority Team (Regular Sales Reps)**
> Probability ≥ 20
> AND Probability < 50
> AND Email Quality is set
**New Lead Team (Junior Sales Reps)**
> Probability < 20
> AND Source contains "website"

## Lead Tracking and Reporting
### 1. Unattended Leads Report
**Purpose:** Identify leads with overdue or due activities that need immediate attention.
### Step-by-Step Process

1. Go to **CRM → Reporting → Pipeline**
1. Clear all default filters in the search bar
1. Click the **▼** (dropdown) icon → **Add Custom Filter**
1. Create these filter rules:

**Rule 1: Past Due Activities**

* Field: **Activities > Due Date**
* Operator: **≤** (less than or equal to)
* Value: **Today's Date**

**Rule 2: Exclude Unassigned Leads**

* Field: **Salesperson**
* Operator: **is set**

**Rule 3: Specific Sales Team (Optional)**

* Field: **Sales Team**
* Operator: **is in**
* Value: Select your team(s)


5. Ensure **"all"** is selected at the top (match all conditions)
6. Click **Add**
7. Group results by **Salesperson** using the Group By option

### 2. Quality Leads Report
**Purpose:** Compare distribution of high-quality leads among sales team members.
**Define Your Quality Lead Criteria**
Choose criteria that indicate a lead is likely to convert:

* Professional email domain (not gmail.com)
* Phone number provided
* Source from live chat or appointment
* Specific geographic regions
* Certain company sizes

### Step-by-Step Process

1. Go to **CRM → Reporting → Pipeline**
1. Click **▼ → Add Custom Filter**
1. Create these rules:

**Rule 1: Date Range**

* Field: **Created On**
* Operator: **≥** (for start date) or **is between** (for date range)
* Value: Set your desired timeframe

**Rule 2: Exclude Unassigned**

* Field: **Salesperson**
* Operator: **is set**

**Rule 3: Quality Criteria Example**

* Field: **Email**
* Operator: **not like** (does not contain)
* Value: **gmail.com**

**Rule 4: Phone Required**

* Field: **Phone**
* Operator: **is set**


4. Enable Include archived toggle
5. Click Add
6. Group by Salesperson

## 3. Lead Distribution Report
### Purpose: Monitor fair distribution of leads across team members.
### Step-by-Step Process

1. Go to **CRM → Reporting → Pipeline**
1. Remove all default filters
1. Add custom filters:

**Essential Filters:**
**Date Filter**

* Field: **Created on**
* Operator: **≥**
* Value: **01/01/2024** (or your desired start date)

**Sales Team Filter**

* Field: **Sales Team**
* Operator: **contains**
* Value: Your team name

**Contact Method Filter**

* Field: **Phone or Email**
* Operator: **is set**

**Active Status Filter**

* Add branch with "any of" condition:

> * **Active is set**
> * **Active is not set**
4. Group by **Salesperson**
5. View as bar chart or list


## 4. Advanced Features
### Marketing Attribution Reports
Track lead sources and marketing campaign effectiveness:

1. Go to **CRM → Reporting → Leads**
1. Use UTM parameters (Medium, Source, Campaign) for grouping
1. Filter by **Active** status
1. Group by **Source** then **City/Country**

## Reseller Management
For businesses with partner networks:

1. Install **Resellers** module from Apps
1. Configure **Partner Levels** (Gold, Silver, Bronze)
1. Set **Level Weight** for automatic assignment probability
1. Assign leads to partners based on location and level


### Sample Scenarios to Practice
**Scenario 1: Weekly Team Review**

1. Create an **Unattended Leads Report** for your team
1. Identify leads with overdue activities
1. Assign follow-up tasks to appropriate team members

**Scenario 2: Monthly Quality Assessment**

1. Run a **Quality Leads Report** for the past 30 days
1. Compare lead quality distribution among team members
1. Adjust assignment rules if imbalance is found

**Scenario 3: Quarterly Performance Analysis**

1. Generate a **Lead Distribution Report** for the quarter
1. Analyze conversion rates by salesperson
1. Create **Marketing Attribution Report** to identify best-performing sources

**Scenario 4: New Team Member Integration**

1. Create assignment rules for new junior sales rep
1. Set probability threshold at **< 20%** for learning opportunities
1. Monitor their progress with weekly unattended leads reports


### Key Metrics to Monitor

* **Lead Response Time:** Time between lead creation and first contact
* **Conversion Rate:** Percentage of leads that become customers
* **Activity Compliance:** Percentage of activities completed on time
* **Lead Distribution Balance:** Even distribution among team members
* **Source Performance:** Which marketing channels generate best leads

# Analyze Performance
### What is CRM Pipeline Analysis?
**Pipeline Analysis** is a tool that helps businesses track and understand how potential customers (leads) move through the sales process from initial contact to final sale or loss. Think of it as a visual roadmap showing where your sales opportunities are and how they're performing.
### Key Terms

* **Lead:** A potential customer who has shown interest in your product/service
* **Opportunity:** A qualified lead with a higher chance of becoming a customer
* **Pipeline Stage:** Different steps in your sales process (e.g., Initial Contact → Qualified → Proposal → Negotiation → Won/Lost)
* **Expected Revenue:** The estimated money value if a deal closes successfully
* **Prorated Revenue:** Expected revenue multiplied by probability of closing


## 1: Pipeline Analysis Basics
### Purpose

* Track lead progression through sales stages
* Identify bottlenecks in your sales process
* Measure team and individual performance
* Make data-driven decisions about resource allocation

### How to Access

1. Open your CRM application
1. Click on **Reporting** tab at the top
1. Select **Pipeline** from the menu

### Understanding the Default View
When you first open Pipeline Analysis, you'll see:

* A bar graph showing leads from the past year
* Each bar represents a pipeline stage
* Colors show which month leads reached each stage
* Numbers indicate how many leads are in each stage

## 2. Customizing Your Analysis
### Step 1: Using Search Filters
The search bar at the top lets you filter your data:
### Quick Filters Available:

* **My Pipeline:** Shows only leads assigned to you
* **Opportunities:** Shows qualified leads only
* **Active/Inactive:** Shows current vs. archived leads
* **Won/Lost:** Shows successful vs. unsuccessful deals
* **Created On:** Filter by when leads were first added
* **Expected Closing:** Filter by when deals are expected to close

### How to Apply Filters:

1. Click the dropdown arrow next to the search bar
1. Select your desired filters from the menu
1. The graph updates automatically

### Step 2: Creating Custom Filters
For more specific analysis:

1. Click the dropdown arrow next to the search bar
1. Select **Add Custom Filter**
1. Build your rule using three fields:

> * **First field:** What to filter (e.g., Country, Salesperson, Revenue)
> * **Second field:** Relationship (e.g., "is", "is not", "greater than")
> * **Third field:** The value to compare against



**Example Custom Filter:**

* First field: "Revenue"
* Second field: "is greater than"
* Third field: "0,000"
* Result: Shows only deals worth more than 0,000

### Step 3: Grouping Data
Group your results to see patterns:
**Common Groupings:**

* **By Stage:** See distribution across pipeline stages
* **By Salesperson:** Compare individual performance
* **By Source:** Understand which marketing channels work best
* **By Month:** Track trends over time


## 3. Different View Options
**Graph View (Default)**

* **Bar Chart:** Compare quantities across categories
* **Line Chart:** Show trends over time
* **Pie Chart:** Show proportions of a whole
* **Stacked Option:** Combine multiple data series in one view

**Pivot View**

* Creates a detailed table with customizable rows and columns
* Best for in-depth analysis with multiple variables
* Can export to Excel for further analysis

**List View**

* Shows individual records in a simple list format
* Good for seeing specific deal details
* Useful for data entry and quick reviews

**Cohort View**

* Groups data by creation date and closing date
* Shows how groups of leads perform over time
* Helps identify seasonal patterns


## 4. Measurement Options
Change what you're measuring by clicking **Measures:**

* **Count:** Number of leads/opportunities
* **Expected Revenue:** Total potential value
* **Days to Close:** How long deals take to complete
* **Days to Convert:** Time from lead to opportunity
* **Recurring Revenue:** Ongoing subscription value


## 5. Creating Specific Reports
### Win/Loss Report
**Purpose:** Compare successful vs. unsuccessful deals to identify improvement areas
### Step-by-Step Process:

1. Go to **CRM → Reporting → Pipeline**
1. Click search dropdown → Select **Stage** under Group By
1. Click **Add Custom Filter**
1. Create two rules:

> * Rule 1: "Active is set"
> * Rule 2: "Active is not set"


5. Set filter to match "any" of the rules
6. Click **Add**

**What You'll See:** Bars showing won and lost deals grouped by pipeline stage
**Sample Questions This Answers:**

* At which stage do we lose most deals?
* What's our overall win rate?
* Which stages need attention?

## Expected Revenue Report
**Purpose:** Forecast upcoming sales based on deals in your pipeline
### Step-by-Step Process:

1. Go to **CRM → Reporting → Pipeline**
1. Click **Measures** → Select **Expected Revenue**
1. Click search dropdown → **Add Custom Filter**
1. Create these rules:

> * "Expected Closing is set"
> * "Expected Closing is between [start date] and [end date]"
> * "Salesperson is set" (to exclude unassigned leads)


5. Set to match "all" rules
6. Click **Add**

**What You'll See:** Total expected revenue grouped by your chosen criteria
**Sample Questions This Answers:**

* How much revenue can we expect this month?
* Which salesperson has the highest potential revenue?
* Are we on track to meet our targets?


## 6. Forecast Reports
### What is Forecasting?
Forecasting shows upcoming opportunities in a visual timeline, helping you predict future sales and adjust expectations.
### How to Access

1. Go to **CRM → Reporting → Forecast**

### Understanding Forecast View

* Shows opportunities grouped by expected closing month
* Displays as cards you can drag between months
* Shows **prorated revenue** at the top of each column

**Prorated Revenue Formula**
> Expected Revenue × Probability = Prorated Revenue

**Example:**

* Deal worth 0,000 with 70% probability = ,000 prorated revenue

### Using Forecast Reports

1. **Drag and Drop:** Move opportunity cards between months to update closing dates
1. **Monthly Totals:** See total expected revenue for each time period
1. **Probability Adjustments:** Update deal probability as negotiations progress


## 7. Saving and Sharing Reports
### Save to Favorites

1. Configure your report with desired filters and groupings
1. Click search dropdown → **Save current search** under Favorites
1. Name your report
1. Check **Shared** to let others use it
1. Check **Default** to make it your homepage view

### Export Options

* **Excel:** Download pivot tables for offline analysis
* **Dashboard:** Add charts to executive dashboards
* **Spreadsheet:** Link live data to Documents app


### Sample Reports to Try
### 1. Monthly Performance Tracker

* **Filter:** Created On = This Month
* **Group By:** Salesperson
* **Measure:** Count
* **Purpose:** See who's generating the most new leads

### 2. High-Value Deal Analysis

* **Custom Filter:** Expected Revenue > 0,000
* **Group By:** Stage
* **Measure:** Expected Revenue
* **Purpose:** Focus on your biggest opportunities

### 3. Conversion Time Analysis

* **Filter:** Won deals from last quarter
* **Measure:** Days to Close
* **Group By:** Source
* **Purpose:** Identify which lead sources convert fastest

### 4. Team Comparison Report

* **Group By:** Sales Team
* **Measure:** Expected Revenue
* **Filter:** Active = True
* **Purpose:** Compare team performance

### 5. Seasonal Trend Analysis

* **Filter:** Created On = Last 12 months
* **Group By:** Created On (by month)
* **View:** Line Chart
* **Purpose:** Identify seasonal patterns in lead generation

# Optimize your Day-to-Day work
### What is Contact and Lead Enrichment?
**Contact and Lead Enrichment** are powerful Odoo features that automatically gather and populate business information about companies and contacts in your database. These tools save time by filling in corporate data that would otherwise require manual research.
### Key Definitions

* **Partner Autocomplete:** Enriches contact records with corporate data when creating new company contacts
* **Lead Enrichment:** Provides detailed business information for leads based on email domain
* **IAP (In-App Purchase):** Credit-based system used to power these enrichment services
* **Credits:** Virtual currency consumed each time you use enrichment features (1 credit per enrichment)

### Purpose and Benefits

* **Save Research Time:** Automatically gather hard-to-find corporate information
* **Improve Data Quality:** Ensure consistent and complete contact records
* **Enhanced Sales Intelligence:** Get valuable insights about prospects and customers
* **Streamlined Workflow:** Reduce manual data entry and focus on selling


## 1. Partner Autocomplete for Contact Enrichment
### What Information Does Partner Autocomplete Provide?

* Full business name and company logo
* Social media accounts (LinkedIn, Twitter, etc.)
* Company type and founding information
* Industry sectors and business activities
* Number of employees
* Estimated revenue
* Phone numbers and timezone
* Technologies used by the company

### Step-by-Step Setup Process
**Step 1: Enable Partner Autocomplete**

1. Navigate to **Settings app**
1. Scroll to the **Contacts section**
1. Find **Partner Autocomplete** feature
1. Tick the checkbox beside it
1. Click **Save** to activate

### Step 2: Configure Your Credits

1. In the same **Contacts section**, locate **Odoo IAP**
1. Click **View My Services**
1. Purchase credits based on your needs
1. Each enrichment costs 1 credit

### How to Use Partner Autocomplete
### Method 1: By Company Name

1. Open any module where you create contacts (CRM, Sales, etc.)
1. Start typing a company name in the **Customer** field
1. Odoo displays a dropdown with suggested companies
1. Select the correct company from suggestions
1. Contact record automatically populates with corporate data
1. Check the chatter for additional company information

### Method 2: By VAT Number

1. Enter the company's VAT number in the appropriate field
1. Odoo will search and suggest matching companies
1. Select the correct match to populate data

### Important Notes

* Companies **cannot** already exist in your Contacts app before enrichment
* Individual contact information cannot be searched (GDPR compliance)
* Without credits, only website link and logo are populated

## 2. CRM Gamification
### What is CRM Gamification?
**CRM Gamification** is a powerful motivation system in Odoo that turns sales activities into game-like challenges with goals, rewards, and competitions. It helps boost team performance by making work more engaging and rewarding.
### Key Definitions

* **Gamification**: Using game-like elements (points, badges, leaderboards) to motivate people in non-game contexts
* **Challenges**: Time-bound competitions with specific goals and rewards
* **Goals**: Specific targets or metrics that sales teams need to achieve
* **Badges**: Digital rewards awarded for completing challenges or achieving goals
* **Rewards**: Recognition given to users who meet or exceed their targets
* **Periodicity**: How often challenges are evaluated (daily, weekly, monthly)

### Purpose and Benefits

* **Increase Motivation**: Make work more engaging and fun
* **Boost Performance**: Encourage healthy competition among team members
* **Track Progress**: Monitor individual and team achievements
* **Improve Results**: Drive better sales outcomes through targeted goals
* **Recognize Success**: Reward high performers and celebrate achievements
* **Build Team Spirit**: Foster collaboration and friendly competition


## 1. Installation and Setup
### Step 1: Install CRM Gamification Module
### For New Installations

1. Navigate to **Apps** application in Odoo
1. Click the **Search bar** at the top
1. Remove the "Apps" filter if present
1. Type **"CRM Gamification"** in the search box
1. Find the **CRM Gamification** module
1. Click **Install** button
1. Wait for installation to complete

### Automatic Installation

* **Note**: If you already have both CRM and Sales apps installed, the CRM Gamification module installs automatically

### Step 2: Enable Developer Mode

1. Go to **Settings** app
1. Scroll to the bottom of the page
1. Click **Activate the developer** mode link
1. Wait for the page to refresh

### Step 3: Access Gamification Tools

1. Navigate to **Settings app**
1. Look for **Gamification Tool**s section

> * This section only appears when Developer mode is enabled


3. Click on **Gamification Tools** to access the menu


## 2. Creating Badges (Rewards System)
### What are Badges?
**Badges** are digital awards given to users when they complete challenges or achieve specific goals. They serve as recognition and motivation tools.
### Step-by-Step Badge Creation
### Step 1: Access Badge Management

1. Go to **Settings → Gamification Tools → Badges**
1. View existing badges or click **New** to create a new one

### Step 2: Configure Basic Badge Information

1. **Badge Name**: Enter a clear, motivating name

> * Examples: "Top Performer", "Deal Closer", "Lead Generator"


2. **Description**: Write what the badge represents

> * Example: "Awarded for closing 10 deals in a month"



### Step 3: Set Badge Granting Rules
Choose who can award this badge by selecting **Allowance to Grant**:
**Option 1: Everyone**

* Any user can manually grant this badge
* Best for: Peer recognition badges

**Option 2: A selected list of users**

* Only specific users can grant this badge
* Creates **Authorized Users** field
* Best for: Management recognition badges

**Option 3: People having some badges**

* Only users with specific badges can grant this badge
* Creates **Required Badges** field
* Best for: Senior-level recognition

**Option 4: No one, assigned through challenges**

* Badge can only be awarded automatically through challenges
* Best for: Performance-based badges

### Step 4: Set Badge Limitations (Optional)

1. Check **Monthly Limited Spending** if you want to limit badge distribution
1. Enter **Limitation Number** (maximum badges per month per person)

### Sample Badge Examples
**Example 1: Monthly Sales Champion**

* **Name**: "Monthly Sales Champion"
* **Description**: "Awarded to the top salesperson each month"
* **Allowance**: No one, assigned through challenges
* **Use Case**: Automatic reward for top performer

**Example 2: Team Player Badge**

* **Name**: "Team Collaboration Star"
* **Description**: "Recognizes outstanding teamwork and collaboration"
* **Allowance**: A selected list of users (Managers only)
* **Limitation**: 3 badges per month per manager

**Example 3: Quick Closer**

* **Name**: "Lightning Deal Closer"
* **Description**: "For closing deals in under 7 days"
* **Allowance**: No one, assigned through challenges
* **Use Case**: Speed-based achievement


### 3: Creating Challenges (Competitions)
**What are Challenges?**
**Challenges** are time-bound competitions where sales team members compete to achieve specific goals and win rewards.
### Step-by-Step Challenge Creation
### Step 1: Access Challenge Management

1. Navigate to **Settings → Gamification Tools → Challenges**
1. Click **New** to create a new challenge

### Step 2: Name Your Challenge

1. Enter a motivating **Challenge Name**

> * Examples: "Q4 Sales Blitz", "New Year Lead Generation", "Monthly Deal Marathon"



### Step 3: Create Assignment Rules
Define who participates in the challenge:

1. Click the first field under **Assign Challenge to**
1. Select parameters to define participants:

> * **Groups**: Choose user groups (e.g., Sales team)
> * **Department**: Select specific departments
> * **Users**: Choose individual users



### Common Assignment Rule Example:

* **Parameter 1**: Groups
* **Operator**: is in
* **Value**: Sales/User: Own Documents Only
* **Result**: All sales users participate

### Step 4: Set Challenge Timing

1. In **Periodicity** field, choose evaluation frequency:

> * **Once**: Single-time challenge
> * **Daily**: Evaluated every day
> * **Weekly**: Evaluated weekly
> * **Monthly**: Evaluated monthly



### Step 5: Add Goals to Challenge

1. Click **Goals** tab
1. Click **Add a line** to add a goal
1. Choose from **Goal Definition** dropdown:

> * **New Leads**: Track lead generation
> * **Time to Qualify a Lead**: Speed of lead qualification
> * **Days to Close a Deal**: Deal closing speed
> * **New Opportunities**: Opportunity creation
> * **New Sales Orders**: Sales order generation


4. Set **Target** number based on the goal
5. Repeat for additional goals

### Step 6: Configure Rewards

1. Click **Rewards** tab
1. Select badge **For 1st User** (winner)
1. Select badge **For Every Succeeding User **(other achievers)

### Step 7: Launch Challenge

1. Review all settings
1. Click **Start Challenge** button
1. Challenge begins immediately

### Sample Challenge Examples
**Example 1: Monthly Lead Generation Challenge**

* **Name**: "January Lead Generation Championship"
* **Assignment**: All Sales Users
* **Periodicity**: Monthly
* **Goals**:

> * New Leads: Target 20 leads
> * Time to Qualify: Under 2 days


* **Rewards**:

> * 1st Place: "Lead Generation Champion" badge
> * Others: "Lead Hunter" badge



**Example 2: Weekly Deal Closing Sprint**

* **Name**: "Weekly Deal Closing Sprint"
* **Assignment**: Senior Sales Team
* **Periodicity**: Weekly
* **Goals**:

> * New Sales Orders: Target 5 orders
> * Days to Close: Under 14 days


* **Rewards**:

> * 1st Place: "Weekly Winner" badge
> * Others: "Deal Closer" badge



**Example 3: Quarterly Performance Challenge**

* **Name**: "Q1 Sales Excellence Challenge"
* **Assignment**: All Sales Representatives
* **Periodicity**: Once (3 months)
* **Goals**:

> * New Opportunities: Target 50 opportunities
> * New Sales Orders: Target 30 orders
> * Days to Close: Under 21 days


* **Rewards**:

> * 1st Place: "Quarterly Champion" badge
> * Others: "Performance Star" badge




### 4. Pre-configured Goals Explained
### Available CRM Goals
**1. New Leads**

* **Purpose**: Track lead generation activity
* **Measurement**: Number of new leads created
* **Sample Target**: 15 leads per month
* **Best For**: Marketing and prospecting activities

**2. Time to Qualify a Lead**

* **Purpose**: Measure lead qualification speed
* **Measurement**: Average days to qualify leads
* **Sample Target**: Under 3 days
* **Best For**: Improving response time and efficiency

**3. Days to Close a Deal**

* **Purpose**: Track deal closing speed
* **Measurement**: Average days from opportunity to closed deal
* **Sample Target**: Under 30 days
* **Best For**: Accelerating sales cycles

**4. New Opportunities**

* **Purpose**: Monitor opportunity creation
* **Measurement**: Number of new opportunities created
* **Sample Target**: 25 opportunities per month
* **Best For**: Pipeline development

**5. New Sales Orders**

* **Purpose**: Track actual sales results
* **Measurement**: Number of sales orders created
* **Sample Target**: 12 orders per month
* **Best For**: Revenue generation


### 5. Practical Implementation Examples
### Scenario 1: Small Sales Team (5 people)
### Challenge Setup: "Monthly Sales Showdown"

* **Participants**: All 5 sales team members
* **Duration**: Monthly
* **Goals**:

> * New Leads: 10 per person
> * New Opportunities: 8 per person
> * New Sales Orders: 5 per person


* **Rewards**:

> * Winner: "Sales Superstar" badge + 00 gift card
> * 2nd-3rd Place: "Sales Achiever" badge
> * Everyone who meets targets: "Goal Crusher" badge



### Scenario 2: Large Sales Organization (20+ people)
### Challenge Setup: "Quarterly Excellence Program"

* **Participants**: Divided into 4 teams of 5 people each
* **Duration**: Quarterly
* **Goals**:

> * Team New Leads: 200 total
> * Team Opportunities: 150 total
> * Average Days to Close: Under 25 days


* **Rewards:**

> * Winning Team: "Champion Team" badge + team dinner
> * Individual top performer: "MVP" badge + recognition



### Scenario 3: New Employee Motivation
### Challenge Setup: "Rookie Rising Star Program"

* **Participants**: New sales employees (first 90 days)
* **Duration**: Monthly for 3 months
* **Goals**:

> * Month 1: New Leads (5), Time to Qualify (5 days)
> * Month 2: New Leads (8), New Opportunities (5)
> * Month 3: New Opportunities (10), New Sales Orders (3)


* **Rewards**:

> * Each month: Progressive badges ("Rookie", "Rising", "Star")
> * Final achievement: "Fast Starter" badge

## 3. Lead Enrichment for Sales Intelligence
### What Information Does Lead Enrichment Provide?
Lead enrichment gathers the same comprehensive data as Partner Autocomplete but specifically for leads in your CRM pipeline.
### Prerequisites
**Enable Leads Feature**

1. Navigate to **CRM app → Configuration → Settings**
1. Under **CRM section**, activate **Leads** option
1. Click **Save**

### Setup Lead Enrichment

1. Go to **CRM app → Configuration → Settings**
1. Under **Lead Generation section**, tick **Lead Enrichment**
1. Choose your enrichment method:

> * **Enrich leads on demand only**: Manual enrichment per lead
> * **Enrich all leads automatically**: Automatic enrichment every 60 minutes


4. Click **Save**

### Lead Enrichment Methods
### Automatic Enrichment

* Runs every 60 minutes via scheduled action
* Enriches leads based on email domain
* No user action required
* Best for high-volume lead processing

Customizing Automatic Schedule

1. Enable **Developer mode**
1. Go to **Settings → Technical → Automation → Scheduled Actions**
1. Search for "CRM"
1. Click **CRM: enrich leads (IAP)**
1. Modify **Execute Every** field (minimum 5 minutes)

### Manual Enrichment
Single Lead Method

1. Open the lead you want to enrich
1. Click the **Enrich **button in the top menu
1. Lead automatically populates with corporate data
1. Review enriched information in the chatter

Bulk Enrichment Method

1. Navigate to **CRM app → Leads**
1. Click the list view button 
1. Select checkboxes for leads to enrich
1. Click **Action** icon
1. Select **Enrich** from dropdown menu


### 3. Practical Examples and Samples to Try
### Sample 1: Enriching a Technology Company Contact
**Try This**: Create a new contact for "Microsoft"

1. Go to any module with contact creation
1. Type "Microsoft" in the Customer field
1. Select "Microsoft Corporation" from suggestions
1. Observe populated data:

* Full company name and logo
* Technology sector information
* Employee count (100,000+)
* Founded date and revenue estimates



### Sample 2: Lead Enrichment Example
**Try This**: Create a lead with email domain "@adobe.com"

1. Create new lead in CRM
1. Add contact email: "[contact@adobe.com](mailto:contact@adobe.com)"
1. Use manual enrichment or wait for automatic
1. Review enriched data:

* Adobe Inc. company information
* Creative software industry classification
* Corporate contact details



### Sample 3: Bulk Lead Processing
**Try This**: Process multiple leads at once

1. Create 3-5 test leads with different company email domains

* @salesforce.com
* @hubspot.com
* @zendesk.com


2. Select all leads in list view
3. Use bulk enrichment action
4. Compare enriched data across different companies


### 4. Best Practices and Tips
### Optimization Strategies

* **Credit Management**: Monitor usage to avoid unexpected costs
* **Data Verification**: Always verify enriched data accuracy
* **Regular Updates**: Re-enrich important contacts periodically
* **Team Training**: Ensure all users understand the enrichment process

### Troubleshooting Common Issues

* **No Suggestions Appear**: Check internet connection and credit balance
* **Incomplete Data**: Some companies may have limited public information
* **Duplicate Contacts**: Ensure contact doesn't already exist before enrichment

### Cost Management

* Start with manual enrichment to control costs
* Purchase credits in bulk for better pricing
* Monitor usage patterns to optimize automatic settings


### 5. Pricing and Credit Management
### Understanding IAP Credits

* **1 Credit = 1 Enrichment**: Each successful enrichment consumes one credit
* **Enterprise Users**: Get free trial credits with valid subscriptions
* **Credit Packages**: Available in various sizes for different usage needs

### Where to Purchase Credits

1. **From Settings**: Settings app → Contacts → Partner Autocomplete → Buy Credits
1. **From CRM Settings**: CRM app → Configuration → Settings → Lead Generation → Buy Credits
1. **IAP Dashboard**: Settings app → Contacts → Odoo IAP → View My Services

### Monitoring Usage

* Check credit balance regularly in IAP dashboard
* Set up notifications for low credit warnings
* Track ROI by monitoring lead conversion improvements

# Gmail Plugin Integration
### What is the Odoo Gmail Plugin?
The **Odoo Gmail Plugin** is a powerful integration tool that connects your Gmail inbox directly with your Odoo database. This plugin allows you to manage your business processes (contacts, opportunities, tickets, and tasks) without leaving your Gmail interface.
### Key Definitions

* **Gmail Plugin**: A browser extension that adds Odoo functionality to your Gmail sidebar
* **Mail Plugin Feature**: The Odoo setting that enables email plugin integrations
* **Contact Creation**: Converting email senders into Odoo contact records
* **Opportunities**: Sales leads and potential deals tracked in Odoo CRM
* **Tickets**: Customer support requests managed through Odoo Helpdesk
* **Tasks**: Action items and to-do lists managed in Odoo Project

### Purpose and Benefits

* **Unified Workflow**: Work seamlessly between Gmail and Odoo
* **No Information Loss**: All email interactions are tracked in Odoo
* **Improved Efficiency**: Create business records directly from emails
* **Better Customer Management**: Convert emails into actionable business processes
* **Time Saving**: Eliminate switching between applications


## 1. Installation Process
### For Odoo Online Users (Recommended Method)
### Step 1: Access Gmail Add-ons

1. Log into your Gmail account
1. Look for the **side panel** on the right side of your inbox
1. If not visible, click the **arrow icon** at the bottom-right corner
1. Click the **plus sign (+)** icon in the side panel

### Step 2: Find and Install Odoo Plugin

1. Use the search bar to search for **"Odoo"**
1. Locate **"Odoo Inbox Addin"** in results
1. **Alternative:** Visit [Google Workspace Marketplace](https://workspace.google.com/marketplace) directly
1. Click **Install** on the Odoo Inbox Addin
1. Click **Continue** to start installation

### Step 3: Grant Permissions

1. Select the Gmail account you want to connect
1. Click **Allow** to let Odoo access your Google account
1. Wait for the success confirmation popup

## For Odoo On-Premise Users (Advanced Method)
### Step 1: Download Plugin Files

1. Visit the [Odoo Mail Plugins GitHub repository](https://github.com/odoo/mail-client-extensions)
1. Click the green **Code** button
1. Select **Download ZIP**
1. Extract the ZIP file to your computer

### Step 2: Modify Configuration Files

1. Navigate to: mail-client-extensions-master → gmail → src → views
1. Open **login.ts** file in a text editor
1. Delete these three lines:
> if (!/^https:\/\/([^\/?]*\.)?odoo\.com(\/|$)/.test(validatedUrl)) {
>      return notify("The URL must be a subdomain of odoo.com");
> }

4. Open **appsscript.json** file
5. Replace all odoo.com references with your server domain

### Step 3: Deploy as Google Project

1. Follow instructions in the **README.md** file
1. Push files as a Google Apps Script project
1. Share the project with your Gmail account
1. Click **Publish and Deploy from manifest**
1. Click **Install the add-on**


## 2. Configuration and Login
### Step 1: Enable Mail Plugin in Odoo

1. Log into your Odoo database
1. Navigate to **Settings → General Settings**
1. Scroll to the **Integrations** section
1. Activate **Mail Plugin** checkbox
1. Click **Save**

### Step 2: Configure Gmail Integration

1. In Gmail, look for the purple **Odoo icon** in the right sidebar
1. Click on the **Odoo icon** to open the plugin window
1. Click on any email in your inbox
1. Click **Authorize Access** in the plugin window
1. Click **Login** button

### Step 3: Connect to Your Odoo Database

1. Enter your Odoo database URL (e.g., https://mycompany.odoo.com)

> * Important: Use the main URL, not a specific page URL


2. Enter your Odoo login credentials
3. Click Allow to grant Gmail access to Odoo
4. Wait for the "Success!" message
5. Close the confirmation window

### Your Gmail and Odoo are now connected!

## 3. Creating Contacts from Emails
### How Contact Creation Works
When you receive an email from someone not in your Odoo database, the plugin allows you to create a contact record directly from the email.
### Step-by-Step Contact Creation

1. **Select an Email**: Click on any email in your Gmail inbox
1. **Open Plugin Panel**: The Odoo plugin panel appears on the right
1. **View Sender Information**: Plugin displays sender's email and available data
1. **Create Contact**: Click **Create Contact** or **Add to Contacts**
1. **Fill Details**: Complete any additional contact information
1. **Save**: Confirm to create the contact in your Odoo database

### Sample Contact Creation Exercise
**Try This**: Create a contact from a business email

1. Find an email from a business contact (e.g., supplier, customer, partner)
1. Click on the email to select it
1. Use the Odoo plugin to create a new contact
1. Add additional details like company name, phone, address
1. Save and verify the contact appears in your Odoo Contacts app


### 4. The Three Core Services
After creating a contact, the Gmail plugin provides access to three powerful services:
### Service 1: Opportunities (Sales Management)
**What are Opportunities?**
**Opportunities** are potential sales deals tracked in your Odoo CRM system. They represent business prospects that could result in revenue.
### When to Create Opportunities

* Receiving inquiry emails about products/services
* Follow-up emails from potential customers
* Price requests or quotation inquiries
* Meeting requests from prospects

### Step-by-Step Opportunity Creation

1. **Select Email**: Click on an email from a potential customer
1. **Open Plugin**: Access the Odoo plugin panel
1. **Choose Opportunity**: Click Create Opportunity button
1. **Fill Details**:

> * **Opportunity Name**: Descriptive title (e.g., "Website Design Project")
> * **Expected Revenue**: Estimated deal value
> * **Probability**: Likelihood of closing (%)
> * **Expected Closing Date**: Target completion date
> * **Sales Team**: Assign to appropriate team
> * **Salesperson**: Assign responsible person


5. Add Notes: Include email content and additional context
6. Save: Create the opportunity in Odoo CRM

### Sample Opportunity Scenarios
**Example 1: Product Inquiry**

* Email: "I'm interested in your software solutions for small businesses"
* Opportunity: "Small Business Software License"
* Revenue: ,000
* Probability: 30%

**Example 2: Service Request**

* Email: "Can you provide a quote for digital marketing services?"
* Opportunity: "Digital Marketing Package"
* Revenue: 5,000
* Probability: 50%

### Service 2: Tickets (Customer Support)
**What are Tickets?**
**Tickets** are customer support requests managed through Odoo's Helpdesk system. They track issues, complaints, questions, and support interactions.
### When to Create Tickets

* Customer complaints or issues
* Technical support requests
* Product return requests
* General customer service inquiries

### Step-by-Step Ticket Creation

1. **Select Support Email**: Click on a customer support email
1. **Access Plugin**: Open the Odoo plugin panel
1. **Create Ticket**: Click **Create Ticket** button
1. **Configure Ticket**:

> * **Subject**: Clear, descriptive title
> * **Priority**: Low, Normal, High, or Urgent
> * **Helpdesk Team**: Assign to appropriate support team
> * **Assigned To**: Specific support agent
> * **Tags**: Categorize the issue (e.g., "bug", "billing", "technical")
> * **Customer**: Link to existing contact


5. **Add Description**: Include email content and issue details
6. **Set Deadline**: If applicable
7. **Save**: Create ticket in Odoo Helpdesk

### Sample Ticket Scenarios
**Example 1: Technical Issue**

* Email: "The software crashes when I try to export reports"
* Ticket: "Report Export Crash Bug"
* Priority: High
* Team: Technical Support

**Example 2: Billing Question**

* Email: "I don't understand my last invoice"
* Ticket: "Invoice Clarification Request"
* Priority: Normal
* Team: Customer Service

### Service 3: Tasks (Project Management)
**What are Tasks?**
**Tasks** are action items and to-do lists managed in Odoo's Project application. They help organize work and track progress on various activities.
### When to Create Tasks

* Action items from email discussions
* Follow-up activities needed
* Project-related work assignments
* Internal reminders and deadlines

### Step-by-Step Task Creation

1. **Select Relevant Email**: Click on an email requiring action
1. **Open Plugin**: Access the Odoo plugin panel
1. **Create Task**: Click Create Task button
1. **Configure Task**:

> * **Task Title**: Clear, actionable description
> * **Project**: Assign to relevant project
> * **Assigned To**: Team member responsible
> * **Deadline**: Due date for completion
> * **Priority**: Set urgency level
> * **Tags**: Categorize task type
> * **Stage**: Current status (To Do, In Progress, Done)


5. **Add Description**: Include context from email
6. **Set Timeframe**: Estimated hours if applicable
7. **Save**: Create task in Odoo Project

### Sample Task Scenarios
**Example 1: Client Request**

* Email: "Please send me the updated project timeline"
* Task: "Prepare and send project timeline to client"
* Project: "Website Development"
* Deadline: Tomorrow

**Example 2: Internal Action**

* Email: "We need to review the contract terms before signing"
* Task: "Review contract terms for ABC Corp deal"
* Project: "Sales Operations"
* Assigned: Legal Team


## 5: Workflow Examples and Best Practices
### Complete Workflow Example: New Business Inquiry
### Scenario
You receive an email: "Hi, I'm interested in your consulting services for our digital transformation project. Can we schedule a call to discuss requirements and pricing?"
### Step-by-Step Process

1. **Create Contact**:

> * Name: John Smith
> * Company: Tech Innovations Inc.
> * Email: [john@techinnovations.com](mailto:john@techinnovations.com)
> * Phone: Add if available


2. **Create Opportunity**:

> * Name: "Tech Innovations Digital Transformation Consulting"
> * Expected Revenue: 5,000
> * Probability: 40%
> * Expected Closing: 30 days


3. **Create Task**:

> * Title: "Schedule discovery call with Tech Innovations"
> * Project: "Sales Activities"
> * Deadline: Within 2 days
> * Assigned: Sales representative



### Multi-Service Workflow Example
**Scenario**
Existing customer emails: "We're having issues with the new feature you deployed last week, but we're also interested in expanding our service package."
**Process**

1. **Create Ticket**:

> * Subject: "New Feature Issues - Customer XYZ"
> * Priority: High
> * Team: Technical Support


2. **Create Opportunity**:

> * Name: "Service Package Expansion - Customer XYZ"
> * Expected Revenue: 0,000
> * Probability: 70%


3. **Create Task**:

> * Title: "Follow up on expansion interest after resolving technical issue"
> * Deadline: After ticket resolution