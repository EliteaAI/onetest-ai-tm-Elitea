---
id: ELITEA-3852
title: "[EliteaAI/elitea_issues#5808] Error Handling — Invalid attachmentType"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3852: [EliteaAI/elitea_issues#5808] Error Handling — Invalid attachmentType

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit returns a clear error message when an invalid attachmentType is provided.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- File available for upload
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="invalid-type", file=<file>)` with unsupported attachmentType. | Toolkit action returns error. |
| 2 | Verify error response includes validation message. | Error message indicates invalid attachment type. |
| 3 | Verify error message lists allowed values: "test-case" and "test-log". | Error message shows valid attachment types. |
| 4 | Verify no attachment is uploaded. | Test run attachment list unchanged. |

## Expected Final State

- Error returned for invalid attachmentType
- No attachment uploaded
- Clear error message listing valid types (test-case, test-log)

## Pass/Fail Criteria

**Pass:** Error returned; valid types listed; no attachment uploaded.  
**Fail:** No error returned; valid types not listed; unexpected attachment created.
