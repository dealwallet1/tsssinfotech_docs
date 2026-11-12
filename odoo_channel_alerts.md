

## Odoo Channel Alerts via API

Post alert messages into an Odoo Discuss channel using a `curl` command.

## Requirement

Alerts must be posted to a Discuss channel automatically.

The manager and the team see the alert in the channel.

The alert is sent with a `curl` command, so any script or monitor can trigger it.

## How It Works

A script calls the Odoo `/json/2` API.

The API runs `message_post` on the `discuss.channel` model.

Odoo saves the message and shows it live in the channel.

## Prerequisites

Odoo 19 (the `/json/2` API does not exist in older versions).

A user account that is a member of the target channel.

The server URL, for example `https://ODOO_URL.com`.

The database name.

## Step 1: Create an API Key

Log in to Odoo as the user who will post the alerts.

Open `Preferences` then `Account Security`.

Click `New API Key`.

Give the key a clear name, for example `channel-alerts`.

Copy the key immediately. It is shown only once.

Paste it without spaces or a trailing line break.

## Step 2: Add the User to the Channel

Open the target channel in Discuss.

Add the API key's user as a member.

For a private channel this is required, or the call fails with an access error.

## Step 3: Find the Channel ID

Open the channel in Discuss.

Check the browser URL. The number at the end is the channel id.

Or call `search_read` on `discuss.channel` with the channel name.

Example: the test channel id used in our testing is `1`.

## Step 4: Build the Request

Method: `POST`

URL: `<ODOO_URL>/json/2/<model>/<method>`

The URL must contain the path only once.

### Headers

`Authorization`: `bearer YOUR_API_KEY`

`X-Odoo-Database`: `your_db_name`

`Content-Type`: `application/json`

### Body

```json
{
  "ids": [<CHANNEL_ID>],
  "body": "<ALERT_MESSAGE>",
  "message_type": "comment",
  "subtype_xmlid": "mail.mt_comment"
}
```

### Field Reference

`ids`: list with the channel id. Square brackets are required.

`body`: the alert text. Send plain text, not HTML.

`message_type`: use `comment`.

`subtype_xmlid`: use `mail.mt_comment`.

## Step 5: Test in Postman

Set the method to `POST` and paste the URL.

In the `Authorization` tab choose `Bearer Token` and paste only the key.

In the `Body` tab choose `raw` and `JSON`, then paste the body.

Click `Send`.

Check that the message appears in the channel.
