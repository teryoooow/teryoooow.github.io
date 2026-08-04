# n8n Practice Workflows

Three small, import-ready n8n workflows built as **personal practice pieces** to demonstrate
workflow-architecture patterns — not client work. Each follows one clear pattern so the logic
is easy to follow in an interview or a demo.

| File | Pattern |
|------|---------|
| `webhook-intake.json` | Webhook → Code-node validation → branch on validity → append to Google Sheets / Slack alert on failure |
| `scheduled-api-to-sheet.json` | Scheduled trigger → HTTP Request (public API) → Code-node transform → append to Google Sheets |
| `error-handler.json` | Error Trigger → normalize error → branch on severity → route alerts (attachable to the other workflows as their error workflow) |

## Setup

1. Import into n8n: **Workflows → Import from File** (or `POST /api/v1/workflows` via the REST API).
2. Replace placeholders:
   - `REPLACE_WITH_GOOGLE_SHEET_ID` — the spreadsheet ID from the sheet URL.
   - `REPLACE_WITH_GOOGLE_CREDENTIAL_ID` / `REPLACE_WITH_SLACK_CREDENTIAL_ID` — credential IDs from
     **Credentials** in n8n (Google OAuth2 + Slack app).
   - `#intake-alerts` / `#critical` / `#errors` — real Slack channels.
3. Activate the workflows (toggle in the editor).
4. Test `webhook-intake.json`: `curl -X POST http://localhost:5678/webhook/intake -H "Content-Type: application/json" -d '{"name":"Test","email":"test@example.com","source":"demo"}'` — valid payloads append to the sheet; invalid ones fire the alert.
5. Attach `error-handler.json` as the **error workflow** of the other two: Workflow settings → Error Workflow.

## Notes

- `scheduled-api-to-sheet.json` uses the Open-Meteo API (no key required) for Angeles City.
- For Telegram alerts instead of Slack: create a **dedicated bot via @BotFather** for n8n — don't
  reuse a bot token that another service is polling with `getUpdates`, or the two pollers conflict.
- The Google Sheets and Slack nodes are the only credential-dependent parts; validation, branching,
  and error formatting run without any credentials, so the architecture is fully demo-able.
