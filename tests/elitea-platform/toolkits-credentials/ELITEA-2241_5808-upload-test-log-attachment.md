---
id: ELITEA-2241
title: "[EliteaAI/elitea_issues#5808] Upload Attachment — Test Log Type"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-2241: [EliteaAI/elitea_issues#5808] Upload Attachment — Test Log Type

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit can successfully upload a file attachment with type "test-log" to a test run.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- Log file available for upload (e.g., execution.log, results.txt)
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a log file for upload (e.g., execution.log, test-results.txt). | File is accessible and ready. |
| 2 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-log", file=<log_file>)`. | Toolkit action executes without error. |
| 3 | Verify response structure: includes testRunId, attachmentType="test-log", filename, fileSize. | Response confirms upload succeeded with correct type. |
| 4 | Verify via qTest API that attachment appears on test run record. | Attachment persisted on qTest backend. |
| 5 | Open qTest UI and navigate to test run; verify attachment is visible with "test-log" label. | Attachment visible in qTest UI with correct type indicator. |

## Expected Final State

- Log file attachment uploaded successfully to test run
- Attachment type set to "test-log"
- Response includes filename confirmation
- Attachment visible on qTest test run record with test-log designation

## Pass/Fail Criteria

**Pass:** Attachment uploaded; type is "test-log"; visible in qTest UI; response confirms details.  
**Fail:** Upload fails; type incorrect; attachment not visible in UI; response missing details.
