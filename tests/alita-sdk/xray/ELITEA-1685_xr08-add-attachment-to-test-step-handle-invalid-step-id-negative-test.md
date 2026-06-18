---
id: ELITEA-1685
title: "XR08 - add_attachment_to_test_step: Handle Invalid Step ID (Negative Test)"
priority: medium
type: functional
module: xray
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1685: XR08 - add_attachment_to_test_step: Handle Invalid Step ID (Negative Test)

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** NEGATIVE TEST: Verify proper error handling when add_attachment_to_test_step receives an invalid step_id format.

Preconditions:
- Xray Cloud integration is configured
- Tool properly validates step_id format before API call

## Preconditions

Xray Cloud integration is configured with valid API credentials.
The tool validates step_id format and rejects non-UUID values.
This is a NEGATIVE test — the expected outcome is a proper error response, not success.

## Test Data

invalid_step_id: "INVALID-123" (non-UUID, intentionally wrong format)
attachment_filename: "test_file.txt"
attachment_content: "Test attachment content"
expected_error_indicators: ["Tool execution error", "invalid", "doesn't exist", "does not exist", "not found", "UUID", "get_tests"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Prepare intentionally invalid step_id: 'INVALID-123' (not a UUID format) | Invalid step_id is set to 'INVALID-123' |
| 3 | Prepare dummy attachment: filename='test_file.txt', content='Test attachment content' | Attachment data is ready |
| 4 | Call `add_attachment_to_test_step` tool with the invalid step_id, filename, and filedata (note: continue_on_error=true so the pipeline does not halt) | Tool returns an error response instead of crashing the pipeline |
| 5 | Verify the error response is non-empty (length > 10 chars) and contains at least one expected error indicator such as 'invalid', 'doesn’t exist', 'UUID', 'get_tests', or 'Tool execution error' | Error message is meaningful and describes the problem |
| 6 | LLM validator verifies negative test criteria: has_error_message=true, error_message_meaningful=true, no_attachment_added=true, no_success_indicators=true | test_results: {test_passed: true, tool_executed: true, has_error_message: true, error_message_meaningful: true, no_attachment_added: true, no_success_indicators: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, has_error_message: true, error_message_meaningful: true, no_attachment_added: true, no_success_indicators: true}

## Pass/Fail Criteria

test_passed = true (NEGATIVE test — error handling is working)
tool_executed = true
has_error_message = true (result length > 10 chars)
error_message_meaningful = true (contains: "Tool execution error", "invalid", "doesn't exist", "UUID", or "get_tests")
no_attachment_added = true
no_success_indicators = true
