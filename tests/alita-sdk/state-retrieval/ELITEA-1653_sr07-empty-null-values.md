---
id: ELITEA-1653
title: "SR07 - Empty/Null Values"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, code_node, edge-case, empty, null]
requirements: []
---
# ELITEA-1653: SR07 - Empty/Null Values

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify edge cases with empty strings, empty lists, empty dicts, and null values are handled correctly when accessed from code nodes.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_7_empty_null_values.yaml

## Test Data

empty_string: ""
empty_list: []
empty_dict: {}
null_value: null
Entry point: verify_empty_null (code node)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize pipeline state with edge-case values: empty_string='', empty_list=[], empty_dict={}, null_value=null | State variables are set; empty collections and null value accepted without error |
| 2 | Execute code node 'verify_empty_null'; reads all 4 vars via alita_state.get() | All 4 variables retrieved without error; no default substitution for empty/null values |
| 3 | Code checks: empty_str == '' (empty string check) | empty_string_ok=True; '' not converted to None or missing |
| 4 | Code checks: empty_lst == [] (empty list check) | empty_list_ok=True; [] not converted to None or lost |
| 5 | Code checks: empty_dct == {} (empty dict check) and null_val is None | empty_dict_ok=True, null_is_none=True; null YAML value maps to Python None |
| 6 | Code checks all types: isinstance checks for str, list, dict (not None) | all_types_correct=True; empty containers retain their type |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; all 5 checks True including null_is_none |

## Expected Final State

test_results.test_passed=True; all 5 checks True including null_is_none

## Pass/Fail Criteria

PASS: test_passed=True, all 5 edge-case checks True
FAIL: empty_string is None instead of ''
FAIL: empty_list is None or missing instead of []
FAIL: empty_dict is None or missing instead of {}
FAIL: null_value is not None (e.g. returned as string 'null' or empty string)
