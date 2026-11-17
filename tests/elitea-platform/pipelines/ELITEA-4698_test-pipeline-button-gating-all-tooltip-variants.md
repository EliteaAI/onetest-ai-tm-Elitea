---
id: ELITEA-4698
title: "Test Pipeline Button — Enablement Gating and All Tooltip Variants"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7154, EliteaAI/elitea_issues#7155]
---
# ELITEA-4698: Test Pipeline Button — Enablement Gating and All Tooltip Variants

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Test Pipeline button is enabled only when the flow is fully configured (entry point set, path to End, no missing required fields), and that the disabled tooltip explains exactly what is missing in every state — for saved and unsaved pipelines.

**Coverage:**
- All tooltip variants, saved and unsaved
- Gate is "configured flow", not just "a node exists"
- Entry-point deletion (no automatic reassignment)
- Auto-connect to End on Save
- Unsaved changes: button stays enabled, sending is blocked (see ELITEA-4703)
- See ELITEA-4714 for the main flow

## Preconditions

- Logged in to {{base_url}}
- At least one agent with a single version exists in the project

## Test Data

- Agent node, Task: `Say hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new pipeline; do not save. Hover/click **Test Pipeline**. | Disabled. *"Save the pipeline to test it."* |
| 2 | Save with zero nodes. Hover **Test Pipeline**. | Disabled. *"Add and configure at least one node connected to End."* |
| 3 | Add an Agent node (do not select an agent). Hover **Test Pipeline** — unsaved, then saved. | Disabled in both. *"Configure node 'Agent 1': Select an agent."* Card shows **Not configured** and a red status icon with tooltip *"Select an agent"*. |
| 4 | Select an agent; leave Task empty. Hover **Test Pipeline** — unsaved, then saved. | Disabled in both. *"Configure node 'Agent 1': Fill in the required input: task."* |
| 5 | Fill in Task. | **Test Pipeline is enabled** (works whether saved or not). |
| 6 | Save. | End is connected to the Agent node automatically; Test Pipeline stays enabled; Auto-arrange becomes enabled. |
| 7 | Add a second node, connect it, then delete the entry-point node. Hover **Test Pipeline**. | Disabled. *"Set an entry point to test the pipeline."* — no node is automatically made the entry point. |
| 8 | Make the remaining node the entry point and configure it. | Test Pipeline enabled again. |
| 9 | With a configured, saved pipeline, edit any field without saving. | **Test Pipeline stays enabled.** In the opened panel, sending is blocked: hovering the send button shows *"Save the pipeline to test the latest changes."* |
| 10 | Delete all nodes. | Test Pipeline is disabled again. |

## Expected Final State

Test Pipeline is enabled only for a fully configured flow; each disabled state shows the precise tooltip for what is missing; unsaved edits on a configured pipeline block sending, not the button.

## Pass/Fail Criteria

**Pass:**
- Each state shows its exact tooltip
- Button enables only once the flow is configured
- Deleting the entry point disables the button with the entry-point tooltip
- Unsaved edits keep the button enabled and block sending with the save hint

**Fail:**
- Button enabled while a required field or entry point is missing
- Generic or wrong tooltip for a state
- Unsaved edits allow sending, or disable the button itself
