# Setup Guide

## Prerequisites

- An n8n instance reachable from the internet (this project used a self-hosted instance on Railway)
- A Tally account
- A Google account with Google Sheets
- A Brevo account
- A Telegram account

## 1. Create the Tally form

Create a form with four fields: Full Name, Phone Number, Email Address, and "What services are you interested in?". Note the form ID from the form URL.

## 2. Create the Google Sheet

Create a sheet, for example `SME Lead Tracker`, with these headers in row 1:

`Timestamp | Full Name | Phone Number | Email Address | Services Interested In | Status`

## 3. Set up Brevo

1. Create an API key and keep it private.
2. Verify the sender address or domain you will send from. Brevo will not deliver mail from an unverified sender.

## 4. Create the Telegram bot

1. Open a chat with `@BotFather` and create a bot. Save the token.
2. Send any message to your new bot from your own account, otherwise it cannot message you.
3. Find your numeric chat ID with a bot such as `@userinfobot` or `@idbot`.

## 5. Make sure n8n can receive webhooks

When n8n runs behind a proxy (as on Railway), set the `WEBHOOK_URL` environment variable to your public n8n URL. Without it, n8n may register an internal address with Tally and the trigger will never fire.

## 6. Import and connect

1. In n8n choose **Import from file** and select `workflow/lead-capture.json`.
2. Create credentials for Google Sheets, Brevo and Telegram, and attach them to their nodes.
3. In the Tally Trigger node, select your form.
4. In the Google Sheets node, select your spreadsheet and tab and confirm the column mapping.
5. In the Telegram node, enter your chat ID.
6. Activate the workflow.

## 7. Test

Submit the form once and confirm all three outputs. See [testing.md](testing.md).

## Exporting your own workflow safely

1. Use **Download** on the workflow. n8n exports credential references, not secrets.
2. Open the JSON and search for your email addresses, chat IDs, spreadsheet IDs and any URL containing your instance name. Replace them with placeholders.
3. Never commit API keys or bot tokens.
