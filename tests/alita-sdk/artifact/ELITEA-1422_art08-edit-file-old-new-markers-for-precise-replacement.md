---
id: ELITEA-1422
title: "ART08 - edit_file: OLD/NEW Markers for Precise Replacement"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1422: ART08 - edit_file: OLD/NEW Markers for Precise Replacement

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify that edit_file correctly replaces content using OLD/NEW marker syntax, preserving unchanged lines and updating targeted content.

Preconditions:
- Artifact toolkit is configured with valid credentials
- TEST_BUCKET exists
- A file with known multi-line content is created during the test

## Preconditions

Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
TEST_BUCKET exists.
A file with multi-line content including a replaceable section is created during the test.

## Test Data

filename: auto-generated with timestamp
bucket_name: TEST_BUCKET
initial content: 3-line file (header / old content to replace / footer)
OLD block: 'old content' (Line 2)
NEW block: 'new content after editing'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Call `createFile` with a 3-line file: Line 1 (header), Line 2 ('old content'), Line 3 (footer — unchanged) | File is created with known multi-line content |
| 3 | Prepare file_query using OLD/NEW marker syntax: OLD block contains Line 2 exactly; NEW block contains 'new content after editing' | Edit query string with OLD <<<<...>>>> OLD and NEW <<<<...>>>> NEW markers is ready |
| 4 | Call `edit_file` tool with file_path (filename), bucket_name, and file_query | Edit operation reports applied changes |
| 5 | Call `readFile` to retrieve the updated file content | File content is returned |
| 6 | LLM validator verifies: new_content_present=true ('new content after editing' in result), old_content_absent=true, unchanged lines (header, footer) intact | test_results: {test_passed: true, edit_succeeded: true, new_content_present: true, old_content_absent: true, unchanged_lines_intact: true} |

## Expected Final State

test_results: {test_passed: true, edit_succeeded: true, new_content_present: true, old_content_absent: true, unchanged_lines_intact: true}

## Pass/Fail Criteria

test_passed = true
file_created = true
edit_succeeded = true
new_content_present = true
old_content_absent = true
unchanged_lines_intact = true
no_errors = true
