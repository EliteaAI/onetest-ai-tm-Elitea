---
id: ELITEA-1428
title: "ART04 - listFiles: Verify Bucket Contents"
priority: critical
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1428: ART04 - listFiles: Verify Bucket Contents

**Module:** Artifact · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Artifact toolkit's listFiles tool returns all files in the bucket with correct metadata including filename, size, and content type.

Preconditions:
- Artifact toolkit is configured with valid credentials
- TEST_BUCKET exists
- At least one file exists or is created during the test

## Preconditions

Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
TEST_BUCKET exists.
File name is timestamped for uniqueness.

## Test Data

filename: auto-generated with timestamp (e.g. 'list-test-{timestamp}.txt')
bucket_name: TEST_BUCKET
content: arbitrary known text

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Call `createFile` tool to create a test file with known content in TEST_BUCKET | File is created successfully |
| 3 | Call `listFiles` tool with bucket_name (TEST_BUCKET) | File listing returns without error |
| 4 | Verify the newly created file appears in the listing with correct filename, non-zero size, and content_type metadata | Created file is present in the list with valid metadata |
| 5 | LLM validator checks: file_in_list=true, metadata fields present (filename, size, content_type), no_errors=true | test_results: {test_passed: true, list_succeeded: true, file_in_list: true, metadata_correct: true} |

## Expected Final State

test_results: {test_passed: true, list_succeeded: true, file_in_list: true, metadata_correct: true}

## Pass/Fail Criteria

test_passed = true
file_created = true
list_succeeded = true
file_in_list = true
metadata_correct = true
no_errors = true
