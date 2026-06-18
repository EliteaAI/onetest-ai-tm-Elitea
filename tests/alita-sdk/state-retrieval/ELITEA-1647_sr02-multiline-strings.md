---
id: ELITEA-1647
title: "SR02 - Multiline Strings"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, multiline, code_node, strings]
requirements: []
---
# ELITEA-1647: SR02 - Multiline Strings

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify newlines and multiline string values in state variables are preserved when passed to code nodes.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_2_multiline_strings.yaml

## Test Data

code_snippet: 3-line Python function (def hello(): print/return)
multiline_text: "Line 1
Line 2
Line 3"
simple_newline: "Hello
World"
Entry point: verify_newlines (code node)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize pipeline state with multiline string variables: code_snippet (3-line Python), multiline_text ('Line 1/2/3'), simple_newline ('Hello/World') | State contains all 3 multiline strings with embedded newline characters preserved |
| 2 | Execute code node 'verify_newlines'; code reads all 3 vars and checks isinstance(alita_state, dict) | alita_state is a dict; state_is_dict=True |
| 3 | Code checks each string for presence of newline character (chr(10)): nl in code, nl in text, nl in simple | All 3 strings contain '\n'; newlines were not stripped or escaped during state passing |
| 4 | Code counts lines via split('\n') for each string | code_lines=3, text_lines=3, simple_lines=2 |
| 5 | Verify test_results.test_passed from code node output | test_results.test_passed=True; code_lines=3, text_lines=3, simple_lines=2, code_preview=first 30 chars |

## Expected Final State

test_results.test_passed=True; code_lines=3, text_lines=3, simple_lines=2, code_preview=first 30 chars

## Pass/Fail Criteria

PASS: test_passed=True, code_lines=3, text_lines=3, simple_lines=2
FAIL: Newlines in multiline strings are stripped or escaped during state passing
FAIL: Any string is received as a single line (line count = 1 instead of expected)
