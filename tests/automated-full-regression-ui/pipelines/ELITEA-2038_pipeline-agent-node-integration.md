---
id: ELITEA-2038
title: "Pipeline — Agent Node Integration"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_agent_node_integration.test_agent_node_fresh_attach
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/9e38607f
---

# ELITEA-2038: Pipeline — Agent Node Integration

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that an agent can be attached to a pipeline, an Agent node added and fully configured with input/output and TASK input mapping, and that all configuration persists after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent (e.g., "IssueTriageSpecialist") is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | IssueTriageSpecialist |
| Input variables | normalized_issue, kb_results |
| Output variable | triage_summary |
| TASK Type | F-String |
| TASK Value | Triage this critical GitHub issue. Issue: {normalized_issue} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline | Pipeline is open for editing |
| 2 | Click "Add node" on canvas → select "Agent" (the Tools section no longer has a "+ Agent" button; agents are picked inside the node) | Agent node is added to the canvas |
| 3 | Open the node's "Agents & Pipelines" picker and select an existing agent (e.g., "IssueTriageSpecialist") | Agent is selected in the node |
| 4 | Verify the agent appears in the left panel Tools list | Agent card is listed in Tools (attachment is persisted on Save) |
| 5 | Verify the Agent node panel is open | Node panel shows the Agent picker and the TASK input-mapping field |
| 6 | Verify Agent node panel shows: Agent picker, TASK field (Type+Value); Input and Output comboboxes are in the collapsed "Advanced" section | All listed sections are present |
| 7 | Expand "Advanced" in the node panel | Input and Output comboboxes are visible |
| 8 | Set Input combobox — add state variables "normalized_issue", "kb_results" | Both variables are added to Input |
| 9 | Set Output combobox — add output variable "triage_summary" | "triage_summary" is added to Output |
| 10 | In INPUT MAPPING (REQUIRED 1) → TASK: set Type to "F-String", Value: "Triage this critical GitHub issue. Issue: {normalized_issue}" | TASK mapping is configured |
| 11 | Save pipeline | Pipeline saves without errors |
| 12 | Reload — verify Agent selection, Input, Output, and TASK mapping persist | All Agent node configuration persists after reload |

---

## Expected Final State

The Agent node is fully configured with Agent selection, Input/Output variables, and TASK input mapping, all persisting correctly after save and reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent selection, Input, Output, and TASK mapping all persist after reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any Agent node field is lost after saving.
