---
id: ELITEA-0822
title: "Agent Node Error Message Includes Node Name and Missing input_mapping Parameters"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [rca:missing-functionality, feat:pipeline_nodes, feat:pipelines, r-2.0.1, eng:qa]
requirements: [ProjectAlita/projectalita.github.io#3742]
---
# ELITEA-0822: Agent Node Error Message Includes Node Name and Missing input_mapping Parameters

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the error message for a misconfigured Agent Node includes the node's display name and specifies which `input_mapping` parameter(s) are missing.

**Coverage:**
- Error message contains the agent node display name (not a generic identifier)
- Error message explicitly lists the missing parameter name(s)
- Error is visible in both the run output area and the Run Details popup
- Error is not a generic "execution failed" string

## Preconditions

- Logged in at {{base_url}}
- Private project with pipeline creation rights
- At least one Agent configured in the project Toolkits

## Test Data

- Pipeline name: TC-ErrorContent
- Agent Node display name: Classify Request
- task field: omitted from input_mapping
- chat_history field: configured (any valid value)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create pipeline 'TC-ErrorContent'. Add an Agent Node. In the canvas, rename the node to 'Classify Request'. Assign a valid Agent. | Node shows name 'Classify Request' in the flow canvas. |
| 2 | In the Agent Node config panel, configure chat_history only — leave task omitted from input_mapping. Click Save. | Pipeline saved. |
| 3 | Run the pipeline by sending a message. | Pipeline execution starts and fails. |
| 4 | Read the error text displayed in the run output / chat area. | Error message contains 'Classify Request' (or the node ID) and explicitly mentions 'task' as the missing parameter. |
| 5 | Click the run chipset to open the Run Details popup. Inspect the error section. | The same node-specific error is visible — node name and missing parameter both present. |

## Expected Final State

The same node-specific error is visible — node name and missing parameter both present.

## Pass/Fail Criteria

**Pass:**
- Error message contains the node name (e.g. 'Classify Request') and explicitly mentions 'task' as the missing parameter
- Same detail is visible in the Run Details popup

**Fail:**
- Error is absent or is a generic message with no node name or missing param reference
- Run Details popup shows no error content
