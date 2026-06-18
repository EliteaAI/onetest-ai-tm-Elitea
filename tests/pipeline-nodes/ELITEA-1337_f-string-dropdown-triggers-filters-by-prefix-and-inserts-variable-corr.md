---
id: ELITEA-1337
title: "F-String Dropdown Triggers, Filters by Prefix, and Inserts Variable Correctly Across All Node Types [Parametrized]"
priority: critical
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1337: F-String Dropdown Triggers, Filters by Prefix, and Inserts Variable Correctly Across All Node Types [Parametrized]

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that typing `{` in any F-String field across all node types triggers the state variable dropdown, that typing additional letters filters the list by prefix, and that selecting a variable inserts `{variable_name}` with the closing brace automatically.

**Coverage:**
- `{` triggers dropdown in F-String fields across: LLM (Task, System), Agent (Task, Chat History, Custom Variable), Toolkit (Input Mapping param), MCP (Input Mapping param), HITL (USER MESSAGE, Input), Printer (Message), Decision (Task)
- Dropdown lists all defined state variables
- Typing a letter after `{` narrows the list to matching prefix
- Selecting a variable inserts `{variable_name}` with closing `}` — no dangling syntax
- Value persists after save

## Preconditions

- Logged into {{base_url}}
- Pipeline exists with state variables: `input`, `messages`, `project_id`, `summary_text`
- All node types (LLM, Agent, Toolkit, MCP, HITL, Printer, Decision) added to the pipeline canvas

## Test Data

State variables: input, messages, project_id, summary_text. Variable to select: project_id.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in Flow view. Open the States sidebar and confirm state variables `input`, `messages`, `project_id`, `summary_text` are listed. | All 4 state variables are visible in the States sidebar. |
| 2 | For each node type below, open its configuration panel, set the specified field type to F-String (where a type selector is available), click inside the field and type `{`: - LLM → Task - LLM → System - Agent → Task - Agent → Chat History - Agent → Custom Variable (if defined) - Toolkit → Input Mapping parameter - MCP → Input Mapping parameter - HITL → USER MESSAGE - HITL → Input - Printer → Message - Decision → Task | A dropdown of state variable suggestions appears immediately after typing `{` in each field. |
| 3 | While the dropdown is open, type the letter `p`. | Dropdown narrows to show only variables starting with `p` (e.g., `project_id`). Variables not starting with `p` are hidden. |
| 4 | Select `project_id` from the dropdown. | `{project_id}` is inserted into the field with the closing `}` appended automatically. No dangling `{` or missing `}` remains. |
| 5 | Save the node. Reopen the node configuration. | Field still shows `{project_id}` — value persisted correctly. |

## Expected Final State

Field still shows `{project_id}` — value persisted correctly.

## Pass/Fail Criteria

**Pass:**
- Dropdown appears on `{` in all listed F-String fields across all node types
- Prefix filtering works correctly
- `{variable_name}` inserted with both braces
- Value persists after save

**Fail:**
- Dropdown does not appear in any field
- Dropdown does not filter by prefix
- Closing `}` is missing after selection
- Value does not persist
