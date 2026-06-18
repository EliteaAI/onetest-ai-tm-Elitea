---
id: ELITEA-1629
title: "QT07 - add_file_to_test_case: Upload File Attachment"
priority: medium
type: functional
module: qtest
status: ready
execution_type: automated
tags: [add_file_to_test_case, file-upload, attachment, qtest]
requirements: []
---
# ELITEA-1629: QT07 - add_file_to_test_case: Upload File Attachment

**Module:** Qtest · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the qTest add_file_to_test_case tool uploads a file attachment to a test case. Tests file attachment upload from artifact storage to a test case or test step.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Artifact storage is accessible with a valid file
Write access to the qTest project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Test case: Name='QT07 Attachment Test {timestamp}', 1 step
File path: artifact file path for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create prerequisite test case via create_test_cases with Name='QT07 Attachment Test {timestamp}' and one test step | Test case created with TC- identifier |
| 3 | Extract the TC- identifier and qTest ID from create response | IDs extracted successfully |
| 4 | Invoke add_file_to_test_case with the test case ID and file path from artifact storage | Tool executes without crashing |
| 5 | Validate the response contains attachment confirmation: 'attached', 'upload', 'success', or 'file' | File upload confirmed; no error indicators |
| 6 | Invoke delete_test_case with the qTest ID to clean up | Test case deleted successfully |

## Expected Final State

Test case deleted successfully

## Pass/Fail Criteria

Tool executes without crashes
Response contains 'attached', 'upload', 'success', or 'file'
No error indicators (Unable to upload, not found)
Cleanup succeeds
