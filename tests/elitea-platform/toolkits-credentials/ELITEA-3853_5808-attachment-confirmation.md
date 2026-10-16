---
id: ELITEA-3853
title: "[EliteaAI/elitea_issues#5808] Attachment Upload Confirmation Response"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3853: [EliteaAI/elitea_issues#5808] Attachment Upload Confirmation Response

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit returns a complete confirmation response when an attachment is uploaded, including all required fields.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- File available for upload (e.g., "screenshot_execution.png")
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Upload file named "screenshot_execution.png" with: `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-case", file=<png_file>)`. | Toolkit action executes successfully. |
| 2 | Verify response includes field: `filename="screenshot_execution.png"`. | Filename field present and correct. |
| 3 | Verify response includes field: `attachmentType="test-case"`. | AttachmentType field present and correct. |
| 4 | Verify response includes field: `testRunId=<value>`. | TestRunId field present and matches input. |
| 5 | Verify response includes timestamp/uploadTime field. | Timestamp field present. |
| 6 | Verify response structure is consistent with other toolkit action responses. | Response format matches toolkit standards. |

## Expected Final State

- Complete confirmation response returned
- All required fields present (filename, attachmentType, testRunId, timestamp)
- Response format consistent with other toolkit actions

## Pass/Fail Criteria

**Pass:** All required fields present and correct; format consistent with toolkit standards.  
**Fail:** Missing fields; incorrect values; inconsistent format.
