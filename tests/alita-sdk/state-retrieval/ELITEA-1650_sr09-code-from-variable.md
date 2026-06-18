---
id: ELITEA-1650
title: "SR09 - Code from Variable"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, dynamic_code, code_node, variable]
requirements: []
---
# ELITEA-1650: SR09 - Code from Variable

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify that code stored as a string in a state variable can be dynamically executed by a code node using code.type=variable.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_9_code_from_variable.yaml

## Test Data

code_to_execute: "x=10; y=20; sum_result=x+y; message=f'The sum of {x} and {y} is {sum_result}'; result={...}; result"
html_content: "<ul>\
\\t<li>Item 1</li>\
\\t<li>Item 2</li>\
</ul>"
Entry point: execute_dynamic_code (code, type=variable) → verify_results (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state: code_to_execute (Python computing x=10, y=20, sum=30 with f-string message), html_content with HTML tags and \n\t characters | State variables set; code_to_execute contains multi-line Python code as a string |
| 2 | Execute code node 'execute_dynamic_code' with code.type=variable, code.value=code_to_execute — pipeline loads and executes the Python code stored in the state variable | Code from state variable is executed; result dict {x:10, y:20, sum:30, message, code_executed:True} is returned and stored in test_results |
| 3 | Pipeline transitions to 'verify_results' code node; reads test_results and html_content from alita_state | test_results is a dict with code_executed=True; html_content is a string with HTML tags and whitespace |
| 4 | Code verifies dynamic execution results: code_executed=True, sum==30, 'sum of 10 and 20 is 30' in message | code_executed=True, sum_correct=True, message_correct=True |
| 5 | Code verifies html_content: '<ul>' in html, '<li>' in html, '\n' in html | html_has_tags=True, html_has_newlines=True; HTML string with embedded whitespace preserved |
| 6 | Verify final test_results.test_passed from verify_results code node | test_results.test_passed=True; computed_sum=30, computed_message contains expected string |

## Expected Final State

test_results.test_passed=True; computed_sum=30, computed_message contains expected string

## Pass/Fail Criteria

PASS: test_passed=True, code_executed=True, sum_correct=True, message_correct=True
FAIL: code.type=variable fails to load code from state variable
FAIL: Dynamically executed code raises an exception or does not produce result dict
FAIL: sum is not 30 (code was not executed or variables are wrong)
FAIL: html_content newlines or tags lost during state passing
