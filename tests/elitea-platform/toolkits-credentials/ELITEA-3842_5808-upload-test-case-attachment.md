---
id: ELITEA-3842
title: "[EliteaAI/elitea_issues#5808] Upload Attachment — Test Case Type"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3842: [EliteaAI/elitea_issues#5808] Upload Attachment — Test Case Type

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit can successfully upload a file attachment with type "test-case" to a test run.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- File available for upload (e.g., screenshot.png, PDF document)
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a file for upload (e.g., PDF screenshot or document). | File is accessible and ready. |
| 2 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-case", file=<file_object>)`. | Toolkit action executes without error. |
| 3 | Verify response structure: includes testRunId, attachmentType="test-case", filename, fileSize. | Response confirms upload succeeded. |
| 4 | Verify via qTest API that attachment appears on test run record. | Attachment persisted on qTest backend. |
| 5 | Open qTest UI and navigate to test run; verify attachment is visible with "test-case" label. | Attachment visible in qTest UI. |

## Expected Final State

- File attachment uploaded successfully to test run
- Attachment type set to "test-case"
- Response includes filename confirmation
- Attachment visible on qTest test run record

## Pass/Fail Criteria

**Pass:** Attachment uploaded; type is "test-case"; visible in qTest UI; response confirms details.  
**Fail:** Upload fails; type incorrect; attachment not visible in UI; response missing details.
