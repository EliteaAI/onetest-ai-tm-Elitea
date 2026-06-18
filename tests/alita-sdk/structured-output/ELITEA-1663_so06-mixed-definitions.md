---
id: ELITEA-1663
title: "SO06 - Mixed Definitions"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [mixed_definitions, structured_output, llm_node]
requirements: []
---
# ELITEA-1663: SO06 - Mixed Definitions

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify that string-based type definitions and dict-based type definitions can be mixed together in the same structured output state declaration.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_6_mixed_definitions.yaml

## Test Data

structured_output_dict: {name:'str', tags:'list[str]', data_items:{type:'list[dict]',description:'...'}, count:'int', description:{type:'str',default:'No description'}}
LLM task: "Generate name='Test User', tags list, data_items list, count=42, description"
Entry point: generate_mixed_format (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_mixed_format' invoked with mixed structured_output_dict: name='str' (string format), tags='list[str]' (string format), data_items={type:'list[dict]',...} (dict format), count='int' (string format), description={type:'str',default:'No description'} (dict format) | Pipeline successfully parses mixed-format type definitions without errors |
| 2 | LLM generates: name='Test User', tags=['important','urgent','reviewed'], data_items with id/value items, count=42, description='This is a test' | LLM returns all 5 fields; pipeline stores into state vars using mixed-format type coercion |
| 3 | Code node 'verify_output' reads all 5 vars and applies isinstance checks | type_checks: name_is_str=True, tags_is_list=True, data_items_is_list=True, count_is_int=True, description_is_str=True |
| 4 | Code checks element types: all tags are str, all data_items are dicts | element_checks: tags_all_strings=True, data_items_all_dicts=True |
| 5 | Code checks presence: name not empty, tags non-empty, count > 0 | value_checks: name_present=True, tags_not_empty=True, count_positive=True |
| 6 | Verify test_results.test_passed from code node | test_results.test_passed=True; mixed_format_working=True; both string-format and dict-format definitions work together |

## Expected Final State

test_results.test_passed=True; mixed_format_working=True; both string-format and dict-format definitions work together

## Pass/Fail Criteria

PASS: test_passed=True, mixed_format_working=True, all type and element checks True
FAIL: Any field type mismatch when mixing string-format and dict-format definitions
FAIL: data_items (dict-format) returns wrong type when mixed with string-format fields
FAIL: Optional description field (with default) causes parsing failure
