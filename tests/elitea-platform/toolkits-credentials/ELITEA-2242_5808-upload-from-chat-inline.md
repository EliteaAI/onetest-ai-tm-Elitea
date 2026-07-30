---
id: ELITEA-2242
title: "[EliteaAI/elitea_issues#5808] Upload Attachment from Chat Inline"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-2242: [EliteaAI/elitea_issues#5808] Upload Attachment from Chat Inline

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit can upload a file attachment sourced from an Elitea chat inline attachment.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- Elitea Chat conversation with an inline file attachment available
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Elitea Chat, upload a file as inline attachment (e.g., screenshot.png). | File appears in chat message. |
| 2 | Reference chat attachment in Agent conversation. | Chat attachment is accessible to toolkit. |
| 3 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-case", file=<chat_attachment>)`. | Toolkit action executes; file extracted from chat source. |
| 4 | Verify response includes filename matching original chat attachment. | Response confirms filename from chat source. |
| 5 | Verify via qTest API that attachment appears on test run record. | Attachment from chat successfully persisted on qTest backend. |
| 6 | In qTest UI, verify attachment is visible on test run with correct filename. | Attachment visible in qTest UI. |

## Expected Final State

- Chat inline attachment successfully uploaded to qTest test run
- Filename matches original chat attachment
- Attachment persisted on qTest backend
- Attachment visible in qTest UI

## Pass/Fail Criteria

**Pass:** Chat attachment extracted and uploaded; filename matches; visible in qTest UI.  
**Fail:** Chat attachment not accessible; upload fails; filename mismatch; attachment not visible in UI.
