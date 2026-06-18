---
id: ELITEA-1654
title: "SR08 - Combined Pipeline"
priority: critical
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, integration, code_node, llm_node, smoke]
requirements: []
---
# ELITEA-1654: SR08 - Combined Pipeline

**Module:** State Retrieval · **Priority:** Critical · **Type:** Functional

**Objective:** Full integration test: LLM node generates Python code from a user query, code node receives and processes the LLM output, verifying end-to-end state passing in a real pipeline.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_8_combined_pipeline.yaml

## Test Data

user_query: "Write a Python function to calculate factorial"
iteration_count: 1
metadata: {model: "gpt-4", tokens: 150}
LLM system: "You are a helpful coding assistant. Always wrap code in markdown code blocks..."
Entry point: generate_code (llm) → process_response (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state with user_query, iteration_count=1, metadata dict {model: gpt-4, tokens: 150} | State initialized; all 3 input vars set correctly |
| 2 | Execute LLM node 'generate_code'; uses user_query as task input (type: variable); LLM instructed to always wrap code in ```python blocks | LLM generates factorial function code wrapped in markdown ```python...``` block; output stored in llm_output state var |
| 3 | Verify LLM node output: llm_output is non-empty string containing markdown code block | llm_output is str, '```' present in output |
| 4 | Pipeline transitions to code node 'process_response'; reads llm_output, iteration_count, metadata, user_query from alita_state | All 4 vars retrieved; alita_state is dict, llm_output is str, iteration_count is int, metadata is dict |
| 5 | Code attempts regex extraction of ```python code block from llm_output | code_extracted=True; extracted Python code snippet is not None |
| 6 | Code verifies: user_query_preserved='Write a Python function to calculate factorial', model_name='gpt-4', tokens_value=150 | user_query and metadata preserved correctly through pipeline execution |
| 7 | Verify test_results.test_passed from code node | test_results.test_passed=True; state_is_dict=True, llm_output_is_string=True, has_code_block=True, iteration_is_int=True, metadata_is_dict=True |

## Expected Final State

test_results.test_passed=True; state_is_dict=True, llm_output_is_string=True, has_code_block=True, iteration_is_int=True, metadata_is_dict=True

## Pass/Fail Criteria

PASS: test_passed=True and all component checks True
FAIL: alita_state is not a dict at code node execution
FAIL: LLM output not stored as str or code block markers stripped
FAIL: iteration_count or metadata types are incorrect after passing through LLM node
FAIL: user_query value is modified during pipeline execution
