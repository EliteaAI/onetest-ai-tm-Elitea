---
id: ELITEA-1666
title: "SO04 - Dict Format"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, dict_format, llm_node]
requirements: []
---
# ELITEA-1666: SO04 - Dict Format

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify that dict-based type definitions (with type, description, and default keys) work correctly in LLM structured output state variable declarations.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_4_dict_format.yaml

## Test Data

structured_output_dict (dict format): {title:{type:'str',description:'The title of the report'}, items:{type:'list[dict]',default:[]}, notes:{type:'str',default:''}, status:{type:'str',default:'pending'}}
LLM task: "Generate title='Test Report', item list, notes, status='completed'"
Entry point: generate_with_dict_format (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_with_dict_format' invoked with dict-format structured_output_dict: title={type:'str',description:'...'},  items={type:'list[dict]',default:[]}, notes={type:'str',default:''}, status={type:'str',default:'pending'} | Pipeline correctly parses dict-format type definitions with type/description/default metadata |
| 2 | LLM generates title='Test Report', list of items with name/value, notes='Some notes here', status='completed' | LLM returns all 4 fields; pipeline stores in state vars |
| 3 | Code node 'verify_output' reads title, items, notes, status from alita_state | All 4 vars retrieved; no errors accessing them from dict-format structured output |
| 4 | Code applies type checks: isinstance(title, str), isinstance(items, list), isinstance(notes, str), isinstance(status, str) | type_checks: all 4 = True |
| 5 | Code checks items_are_dicts = all(isinstance(item, dict) for item in items) if items else True | items_are_dicts=True; list[dict] in dict-format also works correctly |
| 6 | Code checks value_checks: title not empty, status not empty | value_checks: title_not_empty=True, items_are_dicts=True, status_not_empty=True |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; dict_format_working=True |

## Expected Final State

test_results.test_passed=True; dict_format_working=True

## Pass/Fail Criteria

PASS: test_passed=True, dict_format_working=True, all type and value checks True
FAIL: Dict-format type definition (with type/description/default keys) not parsed correctly
FAIL: items is not a list or items elements are not dicts
FAIL: title or status is empty/None despite LLM providing values
FAIL: Default values not applied when LLM omits optional fields
