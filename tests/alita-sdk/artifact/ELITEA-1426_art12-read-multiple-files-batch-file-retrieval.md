---
id: ELITEA-1426
title: "ART12 - read_multiple_files: Batch File Retrieval"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1426: ART12 - read_multiple_files: Batch File Retrieval

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify that read_multiple_files correctly reads multiple files in a single batch operation with correct content mapping for each file.

Preconditions:
- Artifact toolkit is configured with valid credentials
- TEST_BUCKET exists
- Three files are created during the test

## Preconditions

Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
TEST_BUCKET exists.
Three distinct files with known unique content are created during the test.

## Test Data

file1: 'batch-file1-{timestamp}.txt' → content: 'Content of file 1'
file2: 'batch-file2-{timestamp}.txt' → content: 'Content of file 2'
file3: 'batch-file3-{timestamp}.txt' → content: 'Content of file 3'
bucket_name: TEST_BUCKET

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Call `createFile` three times to create: batch-file1-{timestamp}.txt ('Content of file 1'), batch-file2-{timestamp}.txt ('Content of file 2'), batch-file3-{timestamp}.txt ('Content of file 3') | All 3 files are created successfully |
| 3 | Call `read_multiple_files` tool with bucket_name (TEST_BUCKET) and file_paths list containing all 3 filenames | Tool executes in a single operation without error |
| 4 | Verify the result maps each filename to its correct content: file1→'Content of file 1', file2→'Content of file 2', file3→'Content of file 3' | All 3 files are correctly mapped with no content mismatch |
| 5 | LLM validator checks all_files_read=true, each content correct, no missing entries | test_results: {test_passed: true, all_files_read: true, content_correct_for_each: true, no_files_skipped: true} |

## Expected Final State

test_results: {test_passed: true, all_files_read: true, content_correct_for_each: true, no_files_skipped: true}

## Pass/Fail Criteria

test_passed = true
all_files_read = true
content_correct_for_each = true
no_files_skipped = true
no_errors = true
