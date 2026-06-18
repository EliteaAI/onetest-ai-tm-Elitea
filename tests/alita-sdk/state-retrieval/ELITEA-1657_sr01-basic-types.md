---
id: ELITEA-1657
title: "SR01 - Basic Types"
priority: critical
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, basic_types, code_node, smoke]
requirements: []
---
# ELITEA-1657: SR01 - Basic Types

**Module:** State Retrieval · **Priority:** Critical · **Type:** Functional

**Objective:** Verify basic primitive types (str, int, float, bool) are correctly passed to and accessible from code nodes via alita_state.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_1_basic_types.yaml

## Test Data

string_var: "Hello World"
integer_var: 42
float_var: 3.14159
boolean_var: true
Entry point: verify_basic_types (code node)
Node: type=code, reads all 4 vars from alita_state, outputs to test_results

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize pipeline state with: string_var='Hello World', integer_var=42, float_var=3.14159, boolean_var=true | State is set; all 4 variables are present with correct initial values |
| 2 | Execute code node 'verify_basic_types' — code checks isinstance(alita_state, dict) | alita_state is a dict (not a JSON string); state_is_dict=True |
| 3 | Code reads string_var, integer_var, float_var, boolean_var from alita_state and performs type checks | type_checks: string_is_str=True, integer_is_int=True, float_is_float=True, boolean_is_bool=True |
| 4 | Code performs value equality checks for all 4 variables | value_checks: string_correct=True, integer_correct=True, float_correct=True (within 0.0001), boolean_correct=True |
| 5 | Verify final test_results output from code node | test_results.test_passed=True, state_is_dict=True, actual_types show correct Python type names (str, int, float, bool) |

## Expected Final State

test_results.test_passed=True, state_is_dict=True, actual_types show correct Python type names (str, int, float, bool)

## Pass/Fail Criteria

PASS: test_results.test_passed is True and all type_checks and value_checks are True
FAIL: alita_state is not a dict (CRITICAL — state passed as serialized string)
FAIL: any primitive type is incorrect (e.g. integer returned as string)
FAIL: any value does not match the initialized state
