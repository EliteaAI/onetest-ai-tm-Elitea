---
id: ELITEA-0836
title: "Nested-first: New Agent node remains unconfigured when nested agent/pipeline with same name exists"
priority: low
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3752, ProjectAlita/projectalita.github.io#3652]
---
# ELITEA-0836: Nested-first: New Agent node remains unconfigured when nested agent/pipeline with same name exists

**Module:** Pipelines · **Priority:** Low · **Type:** Functional

**Objective:** Objective:
Verify that when a nested agent or nested pipeline already attached at the pipeline level has the same name as a subsequently created Agent node, the new node is not auto-configured and no InputMapping is added to its YAML.

Coverage:
- This test applies to both nested agents and nested pipelines.
- Confirms that creating a new Agent node with the same name as an existing nested entity does not automatically inject configuration or InputMapping.

## Preconditions

- Environment: {{base_url}}
- Logged in with pipeline.create, pipeline.edit, agents.create permissions
- A pipeline available for editing with no unsaved changes

## Test Data

- Pipeline: Same name - TC 
- Nested agent/pipeline name: Agent 1
- New Agent node name: Agent 1 (default)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and open or create pipeline "Same name - TC". | Pipeline editor opens |
| 2 | Attach nested agent or pipeline named Agent 1 at the pipeline level. | Pipeline toolkits list shows "Agent 1"; |
| 3 | Add an Agent node with default name "Agent 1" | Agent node appears named "Agent 1" and its config panel shows no agent selected |
| 4 | Open the pipeline YAML view | YAML for the "Agent 1" node contains no InputMapping and no injected fields derived from the pipeline-level toolkit |
| 5 | (Optional) Repeat steps 2–4 for the other entity type if only one type was used initially (agent vs pipeline). | Same results: newly created Agent node remains unconfigured; YAML contains no injected fields. |

## Expected Final State

Same results: newly created Agent node remains unconfigured; YAML contains no injected fields.

## Pass/Fail Criteria

Pass:
- New Agent node is unconfigured; YAML contains no InputMapping or injected tool fields.

Fail:
- Agent node is auto-configured in UI or YAML shows InputMapping or other injected fields for that node.
