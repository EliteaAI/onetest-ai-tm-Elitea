---
id: ELITEA-1115
title: "QTest – Multiple File Formats (.png, .pdf, .txt) Accepted by \"Add file to test case\""
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits]
requirements: [3180]
---
# ELITEA-1115: QTest – Multiple File Formats (.png, .pdf, .txt) Accepted by "Add file to test case"

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the QTest 'Add file to test case' tool accepts multiple file formats when uploading from an Artifact bucket.

## Preconditions

- ELITEA platform accessible
- QTest toolkit configured with 'Add file to test case' tool enabled
- Artifact bucket contains test files: test-file.png, test-file.pdf, test-file.txt
- A valid QTest test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to test case' with test_case_id and filepath /my-bucket/test-file.png | Tool executes successfully; .png file appears on the QTest test case |
| 2 | Invoke 'Add file to test case' with the same test_case_id and filepath /my-bucket/test-file.pdf | Tool executes successfully; .pdf file appears on the QTest test case |
| 3 | Invoke 'Add file to test case' with the same test_case_id and filepath /my-bucket/test-file.txt | Tool executes successfully; .txt file appears on the QTest test case |

## Expected Final State

Tool executes successfully; .txt file appears on the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
