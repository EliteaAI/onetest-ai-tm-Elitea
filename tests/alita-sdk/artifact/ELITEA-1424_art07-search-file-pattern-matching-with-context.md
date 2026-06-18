---
id: ELITEA-1424
title: "ART07 - search_file: Pattern Matching with Context"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1424: ART07 - search_file: Pattern Matching with Context

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify the Artifact toolkit's search_file tool correctly finds text patterns in files and returns context lines around matches.

Preconditions:
- Artifact toolkit is configured with valid credentials
- TEST_BUCKET exists
- A file with known content is created during the test

## Preconditions

Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
TEST_BUCKET exists.
A file with multi-line content including a known searchable pattern is created during the test.

## Test Data

filename: auto-generated with timestamp
bucket_name: TEST_BUCKET
search_pattern: known unique pattern in file content
context_lines: 2 (lines before/after the match)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Create a multi-line test file in TEST_BUCKET with known content including a distinct searchable pattern (e.g. 'SEARCH_TARGET' on a specific line with context lines before and after) | File is created with known content |
| 3 | Call `search_file` tool with: filename, bucket_name, search pattern, and context_lines count | Tool executes without error |
| 4 | Verify the result includes the matching line with the pattern and specified number of context lines surrounding the match | Match line and context lines are returned |
| 5 | LLM validator checks: pattern_found=true, context_lines_returned=true, no_errors=true | test_results: {test_passed: true, search_succeeded: true, pattern_found: true, context_lines_returned: true} |

## Expected Final State

test_results: {test_passed: true, search_succeeded: true, pattern_found: true, context_lines_returned: true}

## Pass/Fail Criteria

test_passed = true
file_created = true
search_succeeded = true
pattern_found = true
context_lines_returned = true
no_errors = true
