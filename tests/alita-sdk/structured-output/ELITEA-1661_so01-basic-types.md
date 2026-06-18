---
id: ELITEA-1661
title: "SO01 - Basic Types"
priority: critical
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, basic_types, llm_node, smoke]
requirements: []
---
# ELITEA-1661: SO01 - Basic Types

**Module:** Structured Output · **Priority:** Critical · **Type:** Functional

**Objective:** Verify LLM structured output correctly populates simple type definitions (str, int, bool, float) into state variables.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/structured_output/tests/test_case_1_basic_types.yaml

## Test Data

LLM task: "Generate: greeting string, number 42, float 3.14, boolean true (sky is blue)"
structured_output_dict: {greeting:'str', count:'int', pi_value:'float', sky_is_blue:'bool'}
Entry point: generate_structured_output (llm) → verify_output (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | LLM node 'generate_structured_output' is invoked with structured_output=true and structured_output_dict: {greeting:'str', count:'int', pi_value:'float', sky_is_blue:'bool'} | LLM receives task to generate greeting string, integer 42, float 3.14, and boolean true |
| 2 | LLM generates structured response and pipeline parses it into state vars: greeting, count, pi_value, sky_is_blue | All 4 output variables populated from LLM structured output; pipeline transitions to verify_output |
| 3 | Code node 'verify_output' reads all 4 vars from alita_state and applies isinstance checks | type_checks: greeting_is_str=True, count_is_int=True, pi_value_is_float=True, sky_is_blue_is_bool=True |
| 4 | Code applies value checks: greeting non-empty, count==42, 3.0 < pi_value < 4.0, sky_is_blue==True | value_checks: greeting_not_empty=True, count_is_42=True, pi_value_reasonable=True, sky_is_blue_true=True |
| 5 | Verify test_results.test_passed from code node output | test_results.test_passed=True; actual_types shows str/int/float/bool |

## Expected Final State

test_results.test_passed=True; actual_types shows str/int/float/bool

## Pass/Fail Criteria

PASS: test_passed=True, all 4 type_checks True, all 4 value_checks True
FAIL: Any field returned as wrong type (e.g. count as str instead of int)
FAIL: count != 42, sky_is_blue != True, or pi_value out of (3.0, 4.0) range
FAIL: greeting is empty or None
