---
id: ELITEA-1335
title: "Variable References Inserted via Dropdown Are Correctly Serialized in YAML and Resolved at Runtime"
priority: critical
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1335: Variable References Inserted via Dropdown Are Correctly Serialized in YAML and Resolved at Runtime

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a variable reference inserted via the dropdown is correctly represented in YAML view (correct type and syntax) and resolves to the actual state value during pipeline execution.

**Coverage:**
- YAML shows `type: fstring` and correct value string with `{variable_name}` — no double braces or malformed syntax
- Variable resolves to its state value at runtime — no literal `{variable_name}` in output
- Run Details confirms correct substitution

## Preconditions

- Logged into {{base_url}}
- Pipeline with state variable `project_id` set to default value `PROJ-123`
- LLM node added and connected to an End node

## Test Data

State variable: project_id = PROJ-123. LLM Task value: `Summarize {project_id}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the LLM node. Set Task field type to F-String. Type `Summarize `, then type `{`, select `project_id` from the dropdown. | Field shows `Summarize {project_id}`. |
| 2 | Save the pipeline. Switch to YAML view. Locate the LLM node `input_mapping` block and find the `task` entry. | YAML shows `type: fstring` and `value: 'Summarize {project_id}'`. No double braces `{{`, no unclosed braces, no escaped characters. |
| 3 | Switch back to Flow view. Run the pipeline via the Chat interface. | Pipeline executes without errors. |
| 4 | Inspect the run output and open Run Details. Locate the LLM node step. | Output does NOT contain literal `{project_id}`. Run Details shows the resolved value `Summarize PROJ-123`. |

## Expected Final State

Output does NOT contain literal `{project_id}`. Run Details shows the resolved value `Summarize PROJ-123`.

## Pass/Fail Criteria

**Pass:**
- YAML correctly shows `type: fstring` with `{project_id}` in value — no malformed syntax
- Runtime output contains `Summarize PROJ-123` — not literal `{project_id}`

**Fail:**
- YAML is malformed (double braces, wrong type)
- Runtime output contains literal `{project_id}` or the node errors
