---
id: ELITEA-3851
title: "[EliteaAI/elitea_issues#5808] Error Handling — Invalid File Source"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3851: [EliteaAI/elitea_issues#5808] Error Handling — Invalid File Source

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit returns a clear error message when file source is invalid or missing.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `upload_attachment_to_test_run(projectId=<valid>, testRunId=<valid>, attachmentType="test-case", file=None)` with null/missing file. | Toolkit action returns error. |
| 2 | Verify error response indicates file is required. | Error message clearly states file source is required. |
| 3 | Verify no attachment is uploaded. | Test run attachment list unchanged. |
| 4 | Verify error message is actionable. | Error message suggests how to provide a file. |

## Expected Final State

- Error returned for missing/invalid file source
- No attachment uploaded
- Clear, actionable error message

## Pass/Fail Criteria

**Pass:** Error returned; file required message; no attachment uploaded; message is actionable.  
**Fail:** No error returned; vague message; unexpected attachment created.
