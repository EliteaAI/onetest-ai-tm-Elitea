---
id: ELITEA-2243
title: "[EliteaAI/elitea_issues#5808] Upload Attachment from Artifacts Bucket"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-2243: [EliteaAI/elitea_issues#5808] Upload Attachment from Artifacts Bucket

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit can upload a file attachment sourced from the Elitea Artifacts bucket.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- File exists in Elitea Artifacts bucket (e.g., /reports/execution-log.txt)
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify file exists in Elitea Artifacts bucket; note file path. | File path confirmed (e.g., artifacts://reports/execution-log.txt). |
| 2 | In Agent conversation, call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-log", file="artifacts://reports/execution-log.txt")`. | Toolkit action executes; file retrieved from Artifacts source. |
| 3 | Verify response includes filename and source confirmation. | Response confirms file from Artifacts source. |
| 4 | Verify via qTest API that attachment appears on test run record. | Attachment from Artifacts successfully persisted on qTest backend. |
| 5 | In qTest UI, verify attachment is visible on test run with correct filename. | Attachment visible in qTest UI. |

## Expected Final State

- Artifacts bucket file successfully uploaded to qTest test run
- Filename matches Artifacts source file
- Attachment persisted on qTest backend
- Attachment visible in qTest UI

## Pass/Fail Criteria

**Pass:** Artifacts file retrieved and uploaded; filename matches; visible in qTest UI.  
**Fail:** Artifacts file not accessible; upload fails; filename mismatch; attachment not visible in UI.
