---
id: ELITEA-1419
title: "ART14 - confluence add_file_to_page: Append File to Page"
priority: critical
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1419: ART14 - confluence add_file_to_page: Append File to Page

**Module:** Artifact · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Confluence add_file_to_page tool uploads a file from artifact storage and appends its reference to the page content.

Preconditions:
- Confluence toolkit is configured with valid credentials
- Artifact toolkit is configured with valid credentials
- Target page ID 140869772 exists in Confluence
- TEST_ARTIFACT_ID points to a valid artifact file

## Preconditions

Confluence toolkit is configured with CONFLUENCE_TOOLKIT_ID and CONFLUENCE_TOOLKIT_NAME.
Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
Target page ID '140869772' exists and is accessible.
TEST_ARTIFACT_ID references a valid file in artifact storage.

## Test Data

page_id: '140869772'
filepath: TEST_ARTIFACT_ID (env var pointing to artifact file)
filename: 'test_upload.txt'
position: 'append'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Confluence toolkit with CONFLUENCE_TOOLKIT_ID and CONFLUENCE_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Set parameters: page_id='140869772', filepath=TEST_ARTIFACT_ID, filename='test_upload.txt', position='append' | Parameters are ready |
| 3 | Call `add_file_to_page` tool with page_id, filepath (artifact ID), filename, and position='append' | Tool executes without throwing an exception |
| 4 | Verify response contains success message with format: 'File uploaded and added to page' including page_id reference and 'View at:' URL | Success message confirms upload and page update |
| 5 | LLM validator checks: file_uploaded=true, page_updated=true, success_message_format_correct=true, view_url_present=true | test_results: {test_passed: true, tool_executed: true, file_uploaded: true, page_updated: true, view_url_present: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, file_uploaded: true, page_updated: true, view_url_present: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
file_uploaded = true
page_updated = true
success_message_format_correct = true
view_url_present = true
