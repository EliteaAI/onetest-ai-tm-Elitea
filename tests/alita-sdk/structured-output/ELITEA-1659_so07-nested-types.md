---
id: ELITEA-1659
title: "SO07 - Nested Types"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, nested_types, llm_node]
requirements: []
---
# ELITEA-1659: SO07 - Nested Types

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify complex nested type definitions like dict[str, list[int]], list of nested dicts, and deeply nested structures work correctly in LLM structured output.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_7_nested_types.yaml

## Test Data

structured_output_dict: {simple_dict:'dict', dict_with_lists:'dict[str,list]', list_of_nested_dicts:'list[dict]', deep_nested:'dict[str,dict]'}
LLM task: "Generate 4 nested structures: simple dict, dict with list values, list of dicts, deeply nested dict"
Entry point: generate_nested_types (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_nested_types' invoked with structured_output_dict: {simple_dict:'dict', dict_with_lists:'dict[str,list]', list_of_nested_dicts:'list[dict]', deep_nested:'dict[str,dict]'} | Pipeline processes complex nested type annotations without error |
| 2 | LLM generates 4 nested structures: simple dict {key1:value1}, dict with list values {numbers:[1,2,3]}, list of dicts [{config:{enabled:true}}], deep nested {level1:{level2:{level3:'deep_value'}}} | LLM returns all 4 nested structures; pipeline stores in state vars |
| 3 | Code node 'verify_output' reads all 4 vars and applies isinstance checks: isinstance(simple_dict, dict), isinstance(dict_with_lists, dict), isinstance(list_of_nested_dicts, list), isinstance(deep_nested, dict) | type_checks: all 4 = True; top-level containers have correct types |
| 4 | Code checks simple_dict: len > 0, all values are strings | simple_dict_has_values=True, simple_dict_values_are_strings=True |
| 5 | Code checks dict_with_lists: len > 0, all values are lists | dict_with_lists_has_values=True, dict_with_lists_values_are_lists=True |
| 6 | Code checks list_of_nested_dicts: non-empty, all elements are dicts; checks deep_nested: non-empty, all values are dicts | list_of_nested_dicts_not_empty=True, elements_are_dicts=True; deep_nested_has_values=True, values_are_dicts=True |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; nested_types_working=True; structure_checks all pass |

## Expected Final State

test_results.test_passed=True; nested_types_working=True; structure_checks all pass

## Pass/Fail Criteria

PASS: test_passed=True, all type_checks and structure_checks True
FAIL: dict[str, list] or dict[str, dict] type annotations not parsed/enforced correctly
FAIL: list_of_nested_dicts elements are not dicts
FAIL: deep_nested structure is flattened instead of preserving nested dict values
FAIL: Any nested container is returned as a JSON string instead of Python object
