---
id: ELITEA-1420
title: "ART13 - get_file_type: Detect File Type from Content"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1420: ART13 - get_file_type: Detect File Type from Content

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify that get_file_type correctly detects file types from content (magic bytes) and returns accurate MIME type, extension, and filename.

Preconditions:
- Artifact toolkit is configured with valid credentials
- TEST_BUCKET exists
- A plain text file is created during the test

## Preconditions

Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
TEST_BUCKET exists.
A plain text file is created during the test.

## Test Data

filename: auto-generated with timestamp (e.g. 'type-test-{timestamp}.txt')
bucket_name: TEST_BUCKET
file content: 'This is plain text content for type detection'
filepath format: /{bucket_name}/{filename}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Call `createFile` with a .txt file containing plain text: 'This is plain text content for type detection' | File is created successfully |
| 3 | Call `get_file_type` tool with filepath parameter in format '/{bucket_name}/{filename}' and bucket_name | Tool executes without error |
| 4 | Verify the result contains: status='success', extension='txt', mime_type containing 'text/plain' or similar text MIME | File type is correctly identified as plain text |
| 5 | LLM validator checks: status_success=true, extension_correct=true, mime_type_correct=true, filename_returned=true | test_results: {test_passed: true, status_success: true, extension_correct: true, mime_type_correct: true, filename_returned: true} |

## Expected Final State

test_results: {test_passed: true, status_success: true, extension_correct: true, mime_type_correct: true, filename_returned: true}

## Pass/Fail Criteria

test_passed = true
status_success = true
extension_correct = true (txt)
mime_type_correct = true (text/plain)
filename_returned = true
no_errors = true
