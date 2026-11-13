# Testing

All tests used sample data on a test form and my own inbox and Telegram account.

## Test cases

| # | Scenario | Expected result | Outcome |
|---|---|---|---|
| 1 | Submit a valid lead | New row in the sheet with status `New Lead` | Passed |
| 2 | Submit a valid lead | Confirmation email arrives naming the service | Passed |
| 3 | Submit a valid lead | Telegram New Lead Alert arrives with all fields | Passed |
| 4 | Submit the same lead twice | Ideally one row | Two rows and two alerts created (see limitations) |
| 5 | Different services (Laundry, Office wash, House wash) | Service shown correctly in each output | Passed |

## What testing surfaced

- Repeated test submissions created duplicate rows. This led to the "no duplicate protection" item in the README.
- Some early test rows contained the form's placeholder labels instead of real values. These came from test runs.
- Telegram sent one alert per execution, so re-running a test produced repeated alerts.
