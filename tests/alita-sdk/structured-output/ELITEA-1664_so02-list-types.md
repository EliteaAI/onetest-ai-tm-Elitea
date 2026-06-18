---
id: ELITEA-1664
title: "SO02 - List Types"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, list_types, llm_node]
requirements: []
---
# ELITEA-1664: SO02 - List Types

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify LLM structured output correctly handles list type variants: list, list[str], list[int], list[bool] in state variable definitions.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_2_list_types.yaml

## Test Data

LLM task: "Generate 3 color names (str), 3 numbers (int), 3 booleans, and a mixed list"
structured_output_dict: {color_names:'list[str]', numbers:'list[int]', flags:'list[bool]', mixed_items:'list'}
Entry point: generate_list_output (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_list_output' is invoked with structured_output_dict: {color_names:'list[str]', numbers:'list[int]', flags:'list[bool]', mixed_items:'list'} | LLM prepared to return 4 lists with typed elements |
| 2 | LLM generates: 3 color names (red/green/blue as strings), 3 numbers (1/2/3 as ints), 3 booleans, and mixed list | LLM returns structured response; pipeline parses into 4 state list variables |
| 3 | Code node 'verify_output' applies isinstance(list) type checks on all 4 vars | type_checks: color_names_is_list=True, numbers_is_list=True, flags_is_list=True, mixed_items_is_list=True |
| 4 | Code checks element types: all(isinstance(x, str) for color_names), all int for numbers, all bool for flags | element_type_checks: color_names_all_strings=True, numbers_all_ints=True, flags_all_bools=True, mixed_items_has_elements=True |
| 5 | Code checks list lengths >= 3 for color_names, numbers, flags | length_checks all True; each typed list has at least 3 elements |
| 6 | Verify test_results.test_passed from code node | test_results.test_passed=True; all type and element checks pass |

## Expected Final State

test_results.test_passed=True; all type and element checks pass

## Pass/Fail Criteria

PASS: test_passed=True, all type_checks True, all element_checks True
FAIL: Any list returned as wrong type or empty
FAIL: color_names elements are not str, numbers elements are not int, flags elements are not bool
FAIL: list length < 3 for any of the 3 typed lists
