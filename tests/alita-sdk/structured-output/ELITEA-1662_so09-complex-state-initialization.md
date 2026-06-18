---
id: ELITEA-1662
title: "SO09 - Complex State Initialization"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, initialization, complex_state, llm_node]
requirements: []
---
# ELITEA-1662: SO09 - Complex State Initialization

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify structured output works correctly when state is pre-populated with complex list objects, simulating real-world data processing scenarios.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_9_complex_state_initialization.yaml

## Test Data

source_data (pre-populated): [{id:'item_1', name:'First Item', value:100}, {id:'item_2', name:'Second Item', value:200}, {id:'item_3', name:'Third Item', value:300}]
structured_output_dict: {processed_data:'list[dict]', summary:'str', total_value:'int'}
LLM fstring task uses {source_data}
Entry point: process_complex_state (llm, fstring) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state with pre-populated source_data list: 3 objects [{id:'item_1',name:'First Item',value:100}, {id:'item_2',name:'Second Item',value:200}, {id:'item_3',name:'Third Item',value:300}] | source_data is a Python list of 3 dicts in initial state; values sum to 600 |
| 2 | LLM node 'process_complex_state' is invoked with fstring task template that embeds {source_data} from state; structured_output_dict: {processed_data:'list[dict]', summary:'str', total_value:'int'} | fstring template interpolates source_data list into LLM prompt; LLM receives the 3 items |
| 3 | LLM processes source_data: adds 'processed:true' to each item, writes summary, calculates total_value = 100+200+300 = 600 | LLM returns structured response with processed_data list, summary string, total_value=600 |
| 4 | Code node 'verify_output' reads source_data, processed_data, summary, total_value from alita_state | source_checks: source_data_is_list=True, source_data_has_items (len==3), source_items_are_dicts=True |
| 5 | Code verifies output: processed_data_is_list=True, processed_data_not_empty=True, processed_items_are_dicts=True, summary_is_str=True, total_value_is_int=True | All output_checks True; processed_data is list of dicts, not list of strings |
| 6 | Code verifies total_value==600 and summary is non-empty | value_checks: total_value_correct=True, summary_not_empty=True |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; complex_state_working=True; complex pre-populated state + fstring + structured_output all work together |

## Expected Final State

test_results.test_passed=True; complex_state_working=True; complex pre-populated state + fstring + structured_output all work together

## Pass/Fail Criteria

PASS: test_passed=True, all source_checks and output_checks True, total_value==600
FAIL: Pre-populated source_data list with complex objects is not accessible in LLM fstring template
FAIL: processed_data is not a list of dicts after structured output parsing
FAIL: total_value != 600 (LLM did not correctly sum 100+200+300)
FAIL: source_data list loses type (items become strings instead of dicts)
