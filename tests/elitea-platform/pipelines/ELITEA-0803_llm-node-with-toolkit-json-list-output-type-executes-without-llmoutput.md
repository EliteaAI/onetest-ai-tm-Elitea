---
id: ELITEA-0803
title: "LLM Node with Toolkit — JSON/List Output Type Executes Without 'LLMOutput has no attribute content' Error"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, eng:backend, r-2.0.3, eng:ai]
requirements: [EliteaAI/elitea_issues#4965]
---
# ELITEA-0803: LLM Node with Toolkit — JSON/List Output Type Executes Without 'LLMOutput has no attribute content' Error

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an LLM node with an attached toolkit and output variable type set to JSON or List executes successfully and maps the structured output to the output variable — without throwing the `'LLMOutput' object has no attribute 'content'` error.

## Preconditions

- User is logged in to ELITEA.
- At least one toolkit is configured and accessible (e.g. a toolkit named `processed-questionnaire` with a `list_files` tool, or any equivalent).
- A pipeline exists or can be created using the following YAML definition as a reference:

```yaml
state:
  file_list:
    type: list
    value: []
  input:
    type: str
  messages:
    type: list
entry_point: LLM 1
nodes:
  - id: LLM 1
    type: llm
    input:
      - input
    input_mapping:
      chat_history:
        type: fixed
        value: []
      system:
        type: fixed
        value: ''
      task:
        type: fixed
        value: 'Get file list and provide it as json output '
    output:
      - file_list
    structured_output: true
    tool_names:
      processed-questionnaire:
        - list_files
    transition: Printer 1
  - id: Printer 1
    type: printer
    final_message: ''
    input_mapping:
      printer:
        type: variable
        value: file_list
    transition: END
```

Note: The `file_list` output variable is of type `list`, `structured_output: true` is set, and a toolkit tool is attached — this is the exact configuration that triggers the bug.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and open an existing pipeline or create a new one. | Pipeline canvas is displayed. |
| 2 | Add an LLM node to the pipeline. | LLM node appears on the canvas. |
| 3 | Open the LLM node configuration and attach any toolkit to it. | Toolkit is attached to the LLM node. |
| 4 | Set the LLM node prompt to: 'Get file list and provide it as json output' | Prompt is saved. |
| 5 | Set the LLM node output variable type to JSON. | Output variable type is set to JSON without errors. |
| 6 | Save the pipeline configuration and run the pipeline. | Pipeline execution completes successfully. The LLM node output variable contains a valid JSON object. No error 'LLMOutput object has no attribute content' is displayed. |
| 7 | Change the LLM node output variable type to List. Update the prompt to: 'Get file list.' Run the pipeline again. | Pipeline execution completes successfully. The LLM node output variable contains a valid list. No error is thrown. |

## Expected Final State

Pipeline execution completes successfully. The LLM node output variable contains a valid list. No error is thrown.

## Pass/Fail Criteria

PASS: All three output types (JSON, List) complete execution without errors and return correct output.
FAIL: JSON or List output type causes 'LLMOutput object has no attribute content' error or any other failure.
