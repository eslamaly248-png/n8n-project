# OMNA People: Recruitment Automation with n8n

A recruitment system built with n8n: candidates apply with a PDF CV, an AI scores each CV and emails the result, and an error handler keeps everything monitored.

**Live site:** https://eslamaly248-png.github.io/n8n-project/ (works while the author's n8n is running; the badge shows Online/Offline)

## Workflows

| Workflow | Trigger | What it does |
|---|---|---|
| Recruitment 1 - Intake | Form | Validates a PDF CV, blocks duplicates, saves it to Drive, logs it to a sheet |
| Recruitment 2 - Batch Evaluation (AI Screening) | Every hour + manual | Extracts CV text (OCR for scans), scores with AI, emails invites, declines or flags for HR |
| Recruitment 3 - Error Handler | Error + schedules | Logs failures, emails alerts, sends a daily digest, checks the queue is moving |
| Status | Webhook (GET) | Tiny endpoint used by the website's Online/Offline badge |

## Services needed

Docker Desktop, n8n, ngrok (free static domain), Google Cloud OAuth client (Sheets, Drive, Gmail), Gemini API key. All have free tiers.

## Import steps

1. Run n8n with Docker and a public ngrok address.
2. In n8n, create a folder and import each file from `workflows-public/` (Create workflow → … → Import from File).
3. Create your own credentials and select them in every node that shows a warning.
4. Replace every `YOUR_ID` with your own Google Sheet or Drive folder.
5. Set Recruitment 3 as the error workflow of the others, then publish everything.
6. Put your Production URLs into `CONFIG` in `index.html`.
