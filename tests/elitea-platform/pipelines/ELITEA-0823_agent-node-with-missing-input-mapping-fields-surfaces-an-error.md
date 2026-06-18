---
id: ELITEA-0823
title: "Agent Node with Missing input_mapping Fields Surfaces an Error"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [rca:missing-functionality, feat:pipeline_nodes, feat:pipelines, r-2.0.1, eng:qa]
requirements: [ProjectAlita/projectalita.github.io#3742]
---
# ELITEA-0823: Agent Node with Missing input_mapping Fields Surfaces an Error

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that running a pipeline with an Agent Node missing `task` or `chat_history` in `input_mapping` produces a visible error and does not silently skip the node.

**Coverage:**
- `task` missing from input_mapping → ToolException raised and surfaced
- `chat_history` missing from input_mapping → ToolException raised and surfaced
- Both `task` and `chat_history` missing → ToolException raised and surfaced
- Pipeline does not complete successfully for any variant

## Preconditions

- Logged in at {{base_url}}
- Private project selected with pipeline creation rights
- At least one Agent configured in the project Toolkits

## Test Data

Parametrized — run once per variant:

| Variant | task configured? | chat_history configured? |
|---|---|---|
| A | No | Yes |
| B | Yes | No |
| C | No | No |

Pipeline name: TC-AgentValidation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create pipeline 'TC-AgentValidation'. Add Agent Node → End. Assign a valid Agent in the node config. | Agent Node added and connected to End. Agent is assigned. |
| 2 | In the Agent Node config panel, configure input_mapping per the current variant — omit the specified field(s) as described in Test Data. Click Save. | Pipeline saved without editor-level validation errors. |
| 3 | Run the pipeline by sending a message. | Pipeline execution starts. |
| 4 | Observe the run output and chat area for any error messages. | An error message is displayed. Run status does not show success. |
| 5 | Click the run chipset to open the Run Details popup. Inspect the error content. Then repeat steps 2–5 for each remaining variant. | Error section is populated with details referencing the missing input_mapping parameter(s) for all three variants. |

## Expected Final State

Error section is populated with details referencing the missing input_mapping parameter(s) for all three variants.

## Pass/Fail Criteria

**Pass:**
- Error is surfaced for all three variants
- No variant completes with success status
- Run Details contains error text referencing the missing input_mapping parameter(s)

**Fail:**
- Pipeline skips the Agent Node silently or completes with success for any variant
- Run Details contains no error or only a generic message
