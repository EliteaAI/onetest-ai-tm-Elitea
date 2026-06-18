---
id: ELITEA-1665
title: "SO03 - List of Objects"
priority: critical
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, list_of_objects, regression, llm_node]
requirements: []
---
# ELITEA-1665: SO03 - List of Objects

**Module:** Structured Output · **Priority:** Critical · **Type:** Functional

**Objective:** Verify LLM structured output correctly handles list[dict] type - the primary fix in commit e45a9003 - producing a list of dict objects populated into state.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
This test validates the primary fix from commit e45a9003 (list[dict] support)
Test pipeline: suites/structured_output/tests/test_case_3_list_of_objects.yaml

## Test Data

LLM task: "Generate 3 user objects (name, age, active), summary string, total_count=3"
structured_output_dict: {users:'list[dict]', summary:'str', total_count:'int'}
Regression commit: e45a9003
Entry point: generate_list_of_objects (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_list_of_objects' invoked with structured_output_dict: {users:'list[dict]', summary:'str', total_count:'int'} | Pipeline parses type 'list[dict]' correctly — this is the primary fix being verified |
| 2 | LLM generates 3 user objects (Alice/Bob/Carol with name, age, active) plus a summary string and total_count=3 | LLM returns structured response with user list and supporting fields |
| 3 | Pipeline stores output in state vars: users (list), summary (str), total_count (int) | users is populated as a Python list, not a string |
| 4 | Code node 'verify_output' checks: isinstance(users, list), len(users)>0, all items are dicts | type_checks: users_is_list=True, users_not_empty=True; user_structure_valid=True (all items are dicts) |
| 5 | Code iterates users list and checks each item has 'name' and 'age' keys | user_details shows each user has is_dict=True, has_name=True, has_age=True |
| 6 | Code verifies primary_fix_working = users_is_list AND users_not_empty AND user_structure_valid | primary_fix_verification.fix_working=True; users_is_list_of_dicts=True |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; regression test passes confirming list[dict] type works correctly |

## Expected Final State

test_results.test_passed=True; regression test passes confirming list[dict] type works correctly

## Pass/Fail Criteria

PASS: test_passed=True, users_is_list_of_dicts=True, fix_working=True
FAIL (regression): users is a list of strings instead of list of dicts — the bug from before commit e45a9003
FAIL: users list is empty
FAIL: user items do not have 'name' key
FAIL: total_count is not an int or summary is not a str
