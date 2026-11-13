# GitHub Setup Guide for Your Two n8n Projects

## Recommended structure: two repositories

Application forms usually ask for one link per project, and a recruiter should land on a README that explains exactly one thing. Create two public repositories:

| Repository name | Description (GitHub "About" box) |
|---|---|
| `n8n-lead-capture-autoresponder` | n8n workflow: form to Google Sheets to Brevo email to Telegram alert for instant lead follow-up |
| `n8n-invoice-payment-followup` | n8n workflow: Airtable invoice to Brevo email, Telegram alert, and automated payment reminders |

**Topics to add** (About box, gear icon): `n8n`, `automation`, `workflow-automation`, `brevo`, `telegram-bot`, `airtable`, `google-sheets`, `low-code`.

## Folder layout (same in both)

```
repo-name/
├── README.md
├── LICENSE
├── .env.example
├── .gitignore
├── workflow/
│   └── <name>.json
└── docs/
    ├── architecture.md
    ├── setup-guide.md
    ├── testing.md
    └── images/
```

## Step by step

### 1. Export the workflows from n8n
Open each workflow, use the menu, then **Download**. Save the files as `workflow/lead-capture.json` and `workflow/invoice-payment-follow-up.json`.

### 2. Sanitise the JSON before committing
Open each file in a text editor and search for:

- Your real email addresses, phone numbers and bank details
- Telegram chat IDs
- Google Sheet IDs and Airtable base IDs (replace with `YOUR_SHEET_ID`, `YOUR_BASE_ID`)
- Your Railway URL (`...up.railway.app`)
- Any API key or token (there should be none, but check)

### 3. Review the screenshots
The images in `docs/images/` are cropped from your uploaded PDFs so browser tabs and chat lists are not visible. I covered the phone and email columns in the Sheet image and the email addresses in the Telegram images. Open every image yourself before publishing and confirm nothing personal is visible. The invoice email shows a placeholder bank account number, so confirm it is not a real one.

### 4. Create and push each repo

```bash
cd n8n-lead-capture-autoresponder
git init
git add .
git commit -m "Initial commit: lead capture and auto-reply workflow"
git branch -M main
git remote add origin https://github.com/<your-username>/n8n-lead-capture-autoresponder.git
git push -u origin main
```

Repeat in the other folder.

### 5. Pin both repos
On your GitHub profile, choose **Customize your pins** and pin both. Put the invoice repo first if it is the stronger demo.

### 6. Add the links to your application
Use the repository URLs directly. In any free-text box, add one line per project, for example:
"Lead capture to instant follow-up automation (n8n, Tally, Google Sheets, Brevo, Telegram): <link>"

## Things to verify before you publish

I wrote the READMEs from your screenshots and case study. Check these against your real workflows and fix anything that differs:

1. **Wait durations.** The READMEs do not state the actual delays. Add them.
2. **What the If and check nodes test.** I described them as paid or unpaid. Confirm the field and value.
3. **What the Airtable Update nodes change.** I described them generally. Add the exact field and value.
4. **Airtable field names.** The schema in `architecture.md` is a suggestion. Replace it with your actual fields.
5. **The Telegram step in the lead workflow.** Your canvas screenshot shows three nodes, while the Telegram alerts show a fourth exists. Confirm the final workflow has the Telegram node and that the export includes it, then replace `01-workflow-canvas.png` with a fresh screenshot.
6. **Test outcomes 5 and 6** in the invoice `testing.md` are marked "To re-verify". Run them and update the outcome.

## Claims I deliberately left out

Your case study says "under 60 seconds", "100% of leads captured", "100% manual work eliminated" and quotes a "9x more likely to convert" statistic. I left these out of the repos because the screenshots show test data, the timing was not measured, and the statistic has no source. Hiring managers notice unsourced numbers. If you time a few runs, add the measured figure. Do not describe either project as serving a live client unless it did.

## Next step that would help most

The internship centres on the FortyGuard Temperature MCP. A third small repository, for example `temperature-agent-demo`, using any MCP server or a public temperature API with Claude Code, would close your biggest gap. Use the same folder layout.
