---
id: ELITEA-1651
title: "SR10 - Large Strings"
priority: medium
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, large_strings, code_node, stress]
requirements: []
---
# ELITEA-1651: SR10 - Large Strings

**Module:** State Retrieval · **Priority:** Medium · **Type:** Functional

**Objective:** Stress test verifying that large string payloads (large JSON responses, HTML documents) are correctly passed to and handled by code nodes without truncation or corruption.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_10_large_strings.yaml

## Test Data

large_json_response: JSON string ~600 chars with status/data/users[3]/pagination/meta
large_html_content: Full HTML doc with head/body/sections/footer (~50 lines)
repeated_pattern: 240-char string with alphanumeric + !@#$%^&*() special chars
Entry point: verify_large_strings (code node)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state with 3 large string vars: large_json_response (~600 chars JSON with 3 users), large_html_content (full HTML doc ~50 lines), repeated_pattern (~240 chars with alphanumeric and special chars) | All 3 large strings set in state without truncation |
| 2 | Execute code node 'verify_large_strings'; reads all 3 strings from alita_state; verifies each is a Python str | json_is_string=True, html_is_string=True, pattern_is_string=True; lengths are correct |
| 3 | Code parses large_json_response with json.loads(); checks structure | json_parseable=True; parsed structure has data.users array with 3 user objects; users_count=3 |
| 4 | Code checks large_html_content: '<!DOCTYPE' present, '<html' and '</html>' present, newline count > 30 | html_has_doctype=True, html_has_tags=True, html_newline_count > 30 |
| 5 | Code checks repeated_pattern length > 0 and '@#$%' present | pattern_has_special=True; repeated string with special characters preserved intact |
| 6 | Verify test_results.test_passed from code node | test_results.test_passed=True; all large-string integrity checks pass |

## Expected Final State

test_results.test_passed=True; all large-string integrity checks pass

## Pass/Fail Criteria

PASS: test_passed=True; all large string checks pass, users_count=3, html_newline_count>30
FAIL: Large JSON or HTML strings are truncated during state passing
FAIL: JSON string is auto-parsed into a dict (should remain a string)
FAIL: Large string content is corrupted or special chars stripped
