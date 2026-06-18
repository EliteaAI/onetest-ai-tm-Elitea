---
id: ELITEA-0290
title: "Artifact Toolkit — Index Data Completes Successfully"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3568]
---
# ELITEA-0290: Artifact Toolkit — Index Data Completes Successfully

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Index Data operation for an Artifacts toolkit completes successfully with a non-zero file count and no errors.

**Coverage:**
- A new index can be created for an Artifacts toolkit with files in the bucket
- Index status reaches "Completed" with a non-zero indexed file count
- No "Index processing error" or "Unable to extract files" error appears

## Preconditions

- Logged in to {{base_url}}
- An Artifacts toolkit exists configured with a bucket containing at least 2 files (e.g., file1.txt, file2.txt)
- The Indexes tab is accessible on the toolkit

## Test Data

- Artifacts toolkit with a populated bucket (e.g., bucket test-bucket containing file1.txt, file2.txt)
- Index name: test-ind (or any available name)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifacts toolkit and open the Indexes tab. | The Indexes tab loads. Existing indexes (if any) are listed. |
| 2 | Click Create Index. Enter a name (e.g., test-ind), select the target bucket, and confirm. | The index is created and appears in the list. |
| 3 | Click Run on the newly created index. | The indexing process starts. Status changes to "In progress". |
| 4 | Wait for the process to complete. Observe the final status and indexed file count. | Status shows "Completed". Indexed file count is greater than 0. No error banner or "Index processing error" message appears. |

## Expected Final State

Status shows "Completed". Indexed file count is greater than 0. No error banner or "Index processing error" message appears.

## Pass/Fail Criteria

**Pass:**
- Index status shows "Completed"
- Indexed file count is greater than 0
- No error banner or "Index processing error" message appears

**Fail:**
- Index status shows "Index processing error"
- Error message contains "Unable to extract files" or "string indices must be integers"
- Indexed file count remains 0 after completion
