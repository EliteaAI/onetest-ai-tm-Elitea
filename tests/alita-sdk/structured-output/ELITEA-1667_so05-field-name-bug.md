---
id: ELITEA-1667
title: "SO05 - Field Name Bug"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, field_name_bug, regression, llm_node]
requirements: []
---
# ELITEA-1667: SO05 - Field Name Bug

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify that field names containing the substring 'list' (e.g. blacklist, playlist, allowlist) do not trigger false type conversion to list type in structured output.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
This test validates the field name bug fix (checking type string vs field name)
Test pipeline: suites/structured_output/tests/test_case_5_field_name_bug.yaml

## Test Data

structured_output_dict: {blacklist:'str', playlist:'str', allowlist:'str', checklist:'list[str]', actual_list:'list'}
LLM task: "Return blacklist='blocked_user_123', playlist='My Favorite Songs', allowlist='approved_item_456', checklist=['item1','item2','item3'], actual_list=['a','b','c']"
Bug: Before fix, 'list' in field_name (not type) triggered list conversion
Entry point: generate_with_list_field_names (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_with_list_field_names' invoked with structured_output_dict: {blacklist:'str', playlist:'str', allowlist:'str', checklist:'list[str]', actual_list:'list'} | Pipeline builds type schema; field names 'blacklist', 'playlist', 'allowlist' contain substring 'list' but their TYPE is 'str' — should NOT trigger list conversion |
| 2 | LLM generates: blacklist='blocked_user_123' (string), playlist='My Favorite Songs' (string), allowlist='approved_item_456' (string), checklist=['item1','item2','item3'], actual_list=['a','b','c'] | LLM returns all 5 fields; pipeline stores into state vars |
| 3 | Code node 'verify_output' reads all 5 vars from alita_state and checks types | All 5 vars retrieved; code begins checking for field-name-based type conversion bug |
| 4 | CRITICAL check: isinstance(blacklist_val, str), isinstance(playlist_val, str), isinstance(allowlist_val, str) | blacklist_is_string=True, playlist_is_string=True, allowlist_is_string=True — field names containing 'list' did NOT trigger conversion to list type |
| 5 | Check that actual list fields are still lists: isinstance(checklist_val, list), isinstance(actual_list_val, list) | checklist_is_list=True, actual_list_is_list=True — fields declared as list type are properly converted |
| 6 | Code verifies bug_fix_verification.field_name_bug_fixed = all 3 string checks True | field_name_bug_fixed=True; explanation shows 'Field names containing list should not trigger type conversion' |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; all 5 type checks pass confirming the bug is fixed |

## Expected Final State

test_results.test_passed=True; all 5 type checks pass confirming the bug is fixed

## Pass/Fail Criteria

PASS: test_passed=True, field_name_bug_fixed=True, all 5 type_checks True
FAIL (regression): blacklist/playlist/allowlist returned as lists instead of strings — the bug where 'list' in field_name triggered false conversion
FAIL: checklist or actual_list is not a list
FAIL: String fields containing 'list' substring are incorrectly converted to list type
