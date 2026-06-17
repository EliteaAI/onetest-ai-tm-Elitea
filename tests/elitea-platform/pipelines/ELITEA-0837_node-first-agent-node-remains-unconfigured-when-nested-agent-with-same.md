---
id: ELITEA-0837
title: "Node-first: Agent Node remains unconfigured when nested agent with same name is attached"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3752, ProjectAlita/projectalita.github.io#3652]
---
# ELITEA-0837: Node-first: Agent Node remains unconfigured when nested agent with same name is attached

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Objective:
Verify that when an Agent node is created first and later a nested agent or nested pipeline with the same name is attached, the Agent node remains unconfigured and the pipeline YAML contains no InputMapping or spurious "tool" field.

Coverage:
- Applicable for both nested agents and nested pipelines.
- Ensures that attaching a nested entity after node creation does not auto-configure the node.

## Preconditions

- Environment: {{base_url}}
- Logged in with pipeline.create, pipeline.edit, agents.create permissions
- Browser: Chrome/Chromium
No unsaved changes in pipeline editor

## Test Data

- Pipeline: Same name - TC (new pipeline)
- Agent Node name: TestCaseCreator
- Nested agent/pipeline to attach: TestCaseCreator(agent)/TestCaseCreator(pipeline)
- URL start point: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and create a new pipeline "Same name - TC". | Pipeline editor opens with an empty canvas |
| 2 | Add an Agent node and set its node name to "TestCaseCreator". | Node appears named "TestCaseCreator"; node config panel shows no toolkit/tool selected |
| 3 | Create agent/pipeline named "TestCaseCreator" | Agent/Pipeline are successfully created |
| 4 | Use the pipeline "Attach nested agent/pipeline" flow to add a nested agent/pipeline named "TestCaseCreator" | Pipeline-level toolkits list shows "TestCaseCreator" attached; the Agent node "TestCaseCreator" remains visually unconfigured and unchanged in its config panel. |
| 5 | Open the pipeline YAML view. | YAML does NOT include an InputMapping section under the Agent node "TestCaseCreator" and does not add a "tool" field for that node. |
| 6 | (Optional) Repeat steps 3–5 for the other entity type if only one was used initially. | Node remains unconfigured; YAML unchanged. |

## Expected Final State

Node remains unconfigured; YAML unchanged.

## Pass/Fail Criteria

Pass:
- Agent node remains unconfigured in UI after attach.
- YAML for that node contains no InputMapping and no spurious "tool" field.

Fail:
- Agent node becomes auto-configured in UI after attach, or YAML shows an InputMapping under that node, or a spurious/missing "tool" field is introduced.
