
## Cloudflare Turnstile Configuration in Odoo
## Overview

This document explains how to configure Cloudflare Turnstile in Odoo Community Edition using system settings only.


## 1. Create Turnstile Site in Cloudflare

### Step 1: Login to Cloudflare
  Open the `Cloudflare` dashboard:
 
  https://dash.cloudflare.com
 
  Login with your account.

### Step 2: Navigate to Turnstile

From the dashboard:

Security → `Turnstile`

Click Add Site

### Step 3: Configure the Site

Provide the following details:

## Site Name:

`Odoo Website`

## Domain:

For local setup:

`localhost`


For production:

`yourdomain.com`


## Widget Mode:

`Managed` (Recommended)

Click Create

### Step 4: Copy Generated Keys

After creation, Cloudflare will generate:

`Site Key`

`Secret Key`

Store both keys securely.

## 2. Configure Turnstile in Odoo

### Step 1: Open Odoo Settings

Log in to your Odoo database.

From the database dashboard, click Settings.

### Step 2: Enable Developer Mode

Go to:

Settings → Activate Developer Mode

### Step 3: Enable Cloudflare Turnstile

Scroll to the Integrations section.

Enable Cloudflare Turnstile.

Click Save.

### Step 4: Get Keys from Cloudflare

Open the Cloudflare Turnstile dashboard.

Select your created Turnstile site.

`Copy the Site Key`.

`Copy the Secret Key`.

### Step 5: Enter Keys in Odoo

Go back to Odoo Settings.

Paste the Site Key into the `Site Key` field.

Paste the Secret Key into the `Secret Key` field.

Click Save.

### Step 6: Confirm Successful Configuration.

After saving:

The Turnstile option should remain enabled.

Both keys should remain saved in their fields.

No error message should appear.

If all the above conditions are correct, Cloudflare Turnstile is successfully configured.
