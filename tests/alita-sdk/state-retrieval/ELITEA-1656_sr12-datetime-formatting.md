---
id: ELITEA-1656
title: "SR12 - DateTime Formatting"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, formatting, code_node, datetime]
requirements: []
---
# ELITEA-1656: SR12 - DateTime Formatting

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify datetime formatting in code node output strings, including regression check for newline handling when datetime objects are embedded in f-string output.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_12_datetime_formatting.yaml

## Test Data

test_data: 1 (number type)
Code: from datetime import datetime; output_string = f\"11\
\
 Test comment {current_date}{current_time}\"
structured_output: true (code node outputs dict captured directly)
Entry point: code_to_catch_bug_with_new_lines → END

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state with test_data=1 (number type) | State set; test_data=1 |
| 2 | Execute code node 'code_to_catch_bug_with_new_lines' with structured_output=true; code imports datetime and creates two datetime.now() instances | datetime objects created without error |
| 3 | Code builds output_string = f"11\n\n Test comment {current_date}{current_time}" using f-string with embedded newlines and datetime objects | output_string is a non-empty string starting with '11\n\n Test comment' followed by formatted datetime values |
| 4 | Code performs 5 validation checks: has_prefix, contains_newlines, has_datetime, is_string, not_empty | All 5 checks = True; specifically contains_newlines=True confirms '\n\n' is preserved in f-string output |
| 5 | Code returns result dict with test_passed, formatted_message, checks dict, message_length; captured via structured_output=True into test_results | test_results is populated with all result fields; test_results.test_passed=True |

## Expected Final State

test_results is populated with all result fields; test_results.test_passed=True

## Pass/Fail Criteria

PASS: test_passed=True, all 5 checks True
FAIL: Output string does not contain "\
\
" (newlines stripped in f-string output)
FAIL: datetime objects format incorrectly or raise exception in f-string
FAIL: output_string does not start with the expected prefix "11\
\
 Test comment"
FAIL: structured_output=true fails to capture dict return from code node
