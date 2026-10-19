# 📘 Configure Google OAuth2 Provider in Odoo (Step-by-Step Guide)

This document explains the complete process of configuring **Google OAuth2 Login** in **Odoo**, enabling users to sign in using their Google accounts.

---

## ✅ Prerequisites

Before starting, ensure you have:

- Admin access to **Odoo**
- Access to **Google Cloud Console**
- Odoo server URL/domain (example: `https://myodoo.com`)
- Module installed: **auth_oauth**

---

## 1️⃣ Enable OAuth Authentication in Odoo

1. Log in to Odoo as Administrator
2. Go to:

   **Settings → General Settings**

3. Search for:

   **OAuth Authentication**

4. Enable it:

   ✅ OAuth Authentication

5. Click:

   **Save**

---

## 2️⃣ Configure Google OAuth Provider in Odoo

1. Go to:

   **Settings → OAuth Providers**

2. You will see available providers such as:

   - Odoo.com Accounts
   - Facebook Graph
   - Google OAuth2
   - Keycloak

3. Click on:

   **Google OAuth2**

4. Enable the provider:

   ✅ Allowed

---

## 3️⃣ Create OAuth Client in Google Cloud Console

### Step 3.1: Open Google Cloud Console
Go to:

📌 **Google Cloud Console → APIs & Services → Credentials**

---

### Step 3.2: Configure OAuth Consent Screen (If not already configured)

1. Go to:

   **APIs & Services → OAuth consent screen**

2. Select:

   - External (for public users)
   - Internal (for organization-only users)

3. Fill required details:

   - App Name
   - Support Email
   - Developer Email

4. Save and continue

---

### Step 3.3: Create OAuth Client ID

1. Go to:

   **APIs & Services → Credentials**

2. Click:

   **Create Credentials → OAuth client ID**

3. Select Application Type:

   ✅ **Web Application**

4. Give a name (example):

   `Odoo Google Login`

---

## 4️⃣ Add Authorized Redirect URI (Very Important)

In the same OAuth Client configuration screen, add the following redirect URI:

```text
https://<your-odoo-domain>/auth_oauth/signin

## ✅ Example Redirect URIs

Use the below format while configuring **Authorized Redirect URI** in Google Cloud Console:

```text
https://myodoo.com/auth_oauth/signin
https://odoo.mycompany.com/auth_oauth/signin
http://localhost:8069/auth_oauth/signin

## ⚠️ Notes (Very Important)

- Redirect URI **must match exactly**
- **No extra /** at the end
- HTTP/HTTPS must match your Odoo URL
- Domain must match the domain used to access Odoo

---

## 5️⃣ Copy Google OAuth Credentials

After creating the OAuth client in **Google Cloud Console**, Google will generate:

- **Client ID**
- **Client Secret**

### Example

#### Client ID
```text
375626974559-xxxxxxxxxxxxxxxx.apps.googleusercontent.com

### Client Secret
```text
GOCSPX-xxxxxxxxxxxxxxxxxxxx

## 📌 Important

- Client ID always ends with:
  ```text
  .apps.googleusercontent.com

- Client Secret usually starts with:
  ```text
  GOCSPX-

## 6️⃣ Enter Google Credentials in Odoo

Return to Odoo:

📍 **Settings → OAuth Providers → Google OAuth2**

Fill the following details:

| Field | Value |
|------|------|
| Client ID | Paste Google Client ID |
| Client Secret | Paste Google Client Secret |
| Allowed | Enable checkbox |

✅ Save the record.

---

## 7️⃣ Verify OAuth Endpoints in Odoo

In the Google OAuth2 provider record, ensure the endpoints are correct:

### Authorization Endpoint
```text
https://accounts.google.com/o/oauth2/auth

### Token Endpoint
```text
https://oauth2.googleapis.com/token

### Scope
```text
email profile

## 8️⃣ Restart Odoo Server (Recommended)

Restarting is recommended to ensure changes reflect properly.

## 9️⃣ Test Login with Google

1. Open your Odoo login page.
2. You should now see:

   ✅ **Sign in with Google**

3. Click it.
4. Google login page will appear.
5. Select your Gmail account and allow access.

