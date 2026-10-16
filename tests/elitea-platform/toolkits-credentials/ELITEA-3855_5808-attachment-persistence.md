---
id: ELITEA-3855
title: "[EliteaAI/elitea_issues#5808] Attachment Persists on Backend"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3855: [EliteaAI/elitea_issues#5808] Attachment Persists on Backend

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that a file attachment uploaded to a test run persists on the qTest backend and remains available after session reload.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- File available for upload (e.g., "execution-report.pdf")
- qTest Toolkit is enabled
- Access to qTest API for verification (GET endpoints)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-log", file=<report_pdf>)` to upload attachment. | Toolkit action succeeds; response confirms upload. |
| 2 | Wait 2 seconds for backend processing. | Backend has time to persist attachment. |
| 3 | Query qTest API: `GET /api/v3/projects/{projectId}/test-runs/{testRunId}/attachments` to retrieve attachments list. | "execution-report.pdf" appears in attachments list. |
| 4 | Reload Elitea page (F5) to clear session. | Page reloads; session cleared. |
| 5 | Query qTest API again to retrieve attachments list. | "execution-report.pdf" still appears in attachments (persisted). |
| 6 | Open qTest UI directly and navigate to test run attachments. | Attachment visible in qTest UI. |

## Expected Final State

- Attachment persisted on qTest backend
- Attachment available after page reload
- Attachment visible in qTest UI

## Pass/Fail Criteria

**Pass:** Attachment persists on backend; available after reload; visible in qTest UI.  
**Fail:** Attachment lost or unavailable; backend query shows removed attachment; UI does not show attachment.
