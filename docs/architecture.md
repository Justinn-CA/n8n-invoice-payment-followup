     # Architecture

## Nodes

| # | Node name | Type | Purpose |
|---|---|---|---|
| 1 | invoice created | Airtable Trigger | Fires when a new record appears in the Invoices table. |
| 2 | mail generated | Code | Builds the HTML invoice email from the record fields. |
| 3 | Send a transactional email | Brevo | Sends the invoice to the client. |
| 4 | alert business | Telegram | Tells the business the invoice was sent. |
| 5 | Wait | Wait | Pauses before the first payment check. |
| 6 | Get a record | Airtable | Re-reads the invoice to get its current status. |
| 7 | If | IF | Splits paid from unpaid. |
| 8 | Payment Received | Brevo | Confirms payment to the client (paid path). |
| 9 | Update record | Airtable | Updates the invoice record before the reminder (unpaid path). |
| 10 | Reminder mail | Brevo | Sends the friendly reminder. |
| 11 | stage2 | Wait | Pauses before the second payment check. |
| 12 | Get record | Airtable | Re-reads the invoice status. |
| 13 | check | IF | Splits paid from still unpaid. |
| 14 | Thank You | Brevo | Thanks the client for paying (paid path). |
| 15 | overdue | Airtable | Marks the invoice as overdue (unpaid path). |
| 16 | overdue mail | Brevo | Sends the overdue notice. |

## Suggested Airtable schema

Adjust names to match your base and the field references in the nodes.

| Field | Type | Notes |
|---|---|---|
| Invoice Number | Text | For example `INV-001` |
| Client Name | Text | |
| Client Email | Email | Recipient of all emails |
| Client Phone | Phone | Shown in the Telegram alert |
| Amount | Number | |
| Issue Date | Date | |
| Due Date | Date | |
| Status | Single select | For example Unpaid, Paid, Overdue |

## Design decisions

- **Airtable as the trigger and source of truth.** The owner works in a familiar table, and creating a record is enough to start the process.
- **Re-reading the record after each wait.** The workflow never assumes payment status. It fetches the latest value each time, so payments recorded in between are respected.
- **Code node for the email.** Generating the HTML in a Code node allows a branded layout with the amount, due date and payment details filled in per invoice.
- **Escalating tone.** Invoice, then friendly reminder, then overdue notice, with a payment confirmation or thank you whenever the invoice is paid.
