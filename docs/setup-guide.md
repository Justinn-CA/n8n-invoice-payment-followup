# Setup Guide

## Prerequisites

- An n8n instance reachable from the internet (this project used a self-hosted instance on Railway)
- An Airtable account
- A Brevo account with a verified sender
- A Telegram account

## 1. Prepare Airtable

Create a base with an `Invoices` table using the schema in [architecture.md](architecture.md). Create a personal access token with read and write access to that base.

## 2. Set up Brevo

1. Create an API key and keep it private.
2. Verify your sender address or domain. Unverified senders are not delivered.

## 3. Create the Telegram bot

1. Create a bot with `@BotFather` and save the token.
2. Send any message to the bot from your account so it can message you.
3. Find your numeric chat ID with a bot such as `@userinfobot` or `@idbot`.

## 4. Make sure n8n can run long workflows

This workflow uses Wait nodes, so executions stay open between checks. Confirm your n8n instance stays running and has persistent storage for execution data.

If n8n runs behind a proxy (as on Railway), set `WEBHOOK_URL` to the public URL of your instance.

## 5. Import and connect

1. In n8n choose **Import from file** and select `workflow/invoice-payment-follow-up.json`.
2. Create credentials for Airtable, Brevo and Telegram and attach them.
3. In the trigger and Airtable nodes, select your base and table.
4. In the Code node, replace the sample business name and payment details with your own.
5. In the Telegram node, enter your chat ID.
6. Set the Wait nodes to short intervals for testing, such as one or two minutes.
7. Activate the workflow.

## 6. Test

Follow [testing.md](testing.md).

## Exporting your own workflow safely

1. Download the workflow from n8n. Credentials are exported as references, not secrets.
2. Search the JSON for real emails, phone numbers, bank details, chat IDs, base IDs and your instance URL. Replace them with placeholders.
3. Never commit API keys or tokens.
