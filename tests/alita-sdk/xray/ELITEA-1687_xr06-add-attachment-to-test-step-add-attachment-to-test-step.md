---
id: ELITEA-1687
title: "XR06 - add_attachment_to_test_step: Add Attachment to Test Step"
priority: medium
type: functional
module: xray
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1687: XR06 - add_attachment_to_test_step: Add Attachment to Test Step

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Xray add_attachment_to_test_step tool successfully adds file attachments to existing test steps.

Preconditions:
- Xray Cloud integration is configured
- Manual test with steps exists (will be created during test)
- User has permission to modify tests

## Preconditions

Xray Cloud integration is configured with valid API credentials.
User has permission to create tests and add attachments.
A Manual test with at least one step is created during the test execution.

## Test Data

test_summary: auto-generated — format: "XR06 Attachment Test {timestamp}-{random_suffix}"
step action: "Test step for attachment"
attachment filename: auto-generated — format: "test-attachment-{timestamp}.txt"
attachment content: multiline text with timestamp and XR06 validation note
labels: ["ELITEA_AI_CREATED", "XR06_TEST"]
step_id: dynamically extracted UUID from create_test result

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Generate unique test summary and build GraphQL mutation to create a Manual test with one step: action='Test step for attachment', result='Step ready for attachment', labeled XR06_TEST and ELITEA_AI_CREATED | GraphQL mutation string is prepared |
| 3 | Call `create_test` tool with the GraphQL mutation to create the test | Test is created with a step; creation result contains step ID in UUID format |
| 4 | Extract the step ID (UUID format, e.g. xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) from the creation result using regex | Valid step UUID is extracted |
| 5 | Prepare attachment: timestamped filename 'test-attachment-{timestamp}.txt' and multiline text content confirming XR06 attachment functionality | Filename and file content are ready |
| 6 | Call `add_attachment_to_test_step` tool with parameters: step_id (UUID), filename, filedata (text content) | Tool executes without exception |
| 7 | LLM validator verifies: tool_executed=true, no_errors=true, attachment_added=true, has_success_message=true | test_results: {test_passed: true, tool_executed: true, no_errors: true, attachment_added: true, has_success_message: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, attachment_added: true, has_success_message: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
attachment_added = true
has_success_message = true
