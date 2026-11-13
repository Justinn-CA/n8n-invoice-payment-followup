# Testing

All tests used sample data (a fictional client, `Char Cleaning Co.`, and invoice `INV-001`) sent to my own inbox and Telegram account.

## Test cases

| # | Scenario | Expected result | Outcome |
|---|---|---|---|
| 1 | Create a new invoice record | Invoice email arrives with correct client, amount and due date | Passed |
| 2 | Create a new invoice record | Telegram alert arrives with client, amount, due date and invoice number | Passed |
| 3 | Leave invoice unpaid through the first wait | Friendly reminder email arrives | Passed |
| 4 | Mark invoice paid before the first check | Payment Received email arrives and the flow ends | Passed |
| 5 | Mark invoice paid before the second check | Thank You email arrives | To re-verify and record |
| 6 | Leave invoice unpaid through the second check | Overdue email arrives and record marked overdue | To re-verify and record |

## What testing surfaced

- Wait nodes made testing slow, so short intervals were used during development.
- Each execution sends a fresh set of emails, so repeated tests produced repeated messages in the inbox and Telegram.
- The Payment Received path on the first check is a separate branch from the Thank You path on the second check, so each needs its own test.
