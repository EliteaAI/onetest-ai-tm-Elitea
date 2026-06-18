---
id: ELITEA-1671
title: "TR14 - Add File To Case Error Handling"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [add_file_to_case, error-handling, negative-test, file-upload, testrail]
requirements: []
---
# ELITEA-1671: TR14 - Add File To Case Error Handling

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the add_file_to_case tool handles invalid/non-existent file paths gracefully. Tests error handling when the specified file artifact does not exist.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
File 'nonexistent-file-tr14.txt' does not exist in the execution environment

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
filepath: nonexistent-file-tr14.txt (intentionally invalid)
filename: missing-file.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a prerequisite test case via add_case in TESTRAIL_SECTION_ID with title '[Auto] Test Case for TR14 - File Error Test' | Test case is created and a case ID is returned |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke add_file_to_case with case_id, filepath='nonexistent-file-tr14.txt', and filename='missing-file.txt' | Tool executes without crashing; returns a response (error expected) |
| 5 | Invoke delete_case with the case ID to clean up | Case is deleted successfully |
| 6 | Validate the add_file_to_case response contains an appropriate error indicating the file was not found or could not be accessed | Error message references the missing file path or download failure; no unhandled exception; no unrelated system errors |

## Expected Final State

Error message references the missing file path or download failure; no unhandled exception; no unrelated system errors

## Pass/Fail Criteria

Tool does not crash or throw unhandled exception
Response contains an error message
Error message indicates file not found, download failed, or path invalid
The prerequisite test case is created and deleted during cleanup
No unrelated system errors
