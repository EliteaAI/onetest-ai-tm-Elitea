---
id: ELITEA-1648
title: "SR06 - LLM Code Blocks"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, code_blocks, markdown, llm_node]
requirements: []
---
# ELITEA-1648: SR06 - LLM Code Blocks

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify LLM-generated content containing markdown code blocks is preserved as a plain string in state and not interpreted or parsed.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_6_llm_code_blocks.yaml

## Test Data

LLM system prompt: "You are a helpful coding assistant. Always wrap code in markdown code blocks with the language specified."
LLM task: "Write a simple Python function called 'add' that takes two parameters a and b and returns their sum."
Output state var: llm_response (str)
Entry point: generate_code (llm) → verify_code_blocks (code)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Execute LLM node 'generate_code' with fixed system/task prompts; LLM is instructed to wrap code in markdown code blocks | LLM generates a response containing Python `add` function wrapped in ```python...``` markdown code block; stored as string in llm_response |
| 2 | Pipeline transitions to code node 'verify_code_blocks'; reads llm_response from alita_state | llm_response is retrieved as a Python str type (not parsed/executed) |
| 3 | Code checks isinstance(response, str) — verifies LLM output is stored as raw string, not interpreted | is_string=True; markdown code blocks are preserved as text |
| 4 | Code checks '```' in response to confirm markdown code block markers are present | has_code_block=True; triple-backtick markers intact in output string |
| 5 | Code counts newlines in response (chr(10)): response.count(nl) >= 2 | newline_count >= 2; has_newlines=True (multiline LLM output preserved) |
| 6 | Verify test_results.test_passed from code node | test_results.test_passed=True; is_string=True, has_code_block=True, has_newlines=True, has_def=True, has_add=True |

## Expected Final State

test_results.test_passed=True; is_string=True, has_code_block=True, has_newlines=True, has_def=True, has_add=True

## Pass/Fail Criteria

PASS: test_passed=True, is_string=True, has_code_block=True, has_newlines=True
FAIL: LLM output is not stored as a string (e.g. parsed into dict or executed as code)
FAIL: Markdown code block backticks are stripped from the stored value
FAIL: Newlines are stripped from LLM multiline output
