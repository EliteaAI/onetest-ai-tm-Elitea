---
id: ELITEA-0365
title: "Pipeline Chat Canvas — Flow and YAML Views Refresh Immediately After Save"
priority: high
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:pipelines, eng:frontend, feat:canvas, feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3919]
---
# ELITEA-0365: Pipeline Chat Canvas — Flow and YAML Views Refresh Immediately After Save

**Module:** Canvas · **Priority:** High · **Type:** Functional

**Objective:** Verify that after saving changes in the Pipeline Chat Canvas, both the Flow and YAML views immediately display the updated data without requiring the canvas to be closed and reopened.

**Coverage:**
- Flow view reflects changes immediately after clicking Save
- YAML view reflects changes immediately after clicking Save
- No stale/outdated data is shown in either view post-save
- Canvas reopen is not required to see the updated state

## Preconditions

- User is logged in to the ELITEA platform
- Environment: {{base_url}}
- Browser: Chrome (latest stable)
- At least one pipeline exists in the project
- A chat conversation with that pipeline is available (or can be created)

## Test Data

- Pipeline: any existing pipeline with at least one node
- Change to make in Flow: add a new node (e.g., an LLM node) or rename an existing node
- Change to make in YAML: edit any field value (e.g., update a node name or parameter)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat that uses a pipeline (or create a new chat and add a pipeline as participant). Open the pipeline canvas from the chat. | Pipeline canvas opens showing the current Flow view. |
| 2 | Note the current state of the Flow (e.g., number of nodes, node names). | Current flow state is visible and noted for comparison. |
| 3 | Make a visible change in the Flow view — e.g., add a new node or rename an existing one. | The change is reflected in the canvas editor. |
| 4 | Click Save. | Save completes successfully (no error shown). |
| 5 | Without closing or reopening the canvas, inspect the Flow view. | The Flow view immediately displays the updated data (the added/renamed node is visible). No outdated state is shown. |
| 6 | Switch to the YAML view within the same canvas session. | The YAML view also immediately reflects the saved changes. The YAML content matches the updated flow state. |
| 7 | Close and reopen the canvas to cross-check. | Both the Flow and YAML views after reopen match what was shown immediately after save — confirming data consistency. |

## Expected Final State

Both the Flow and YAML views after reopen match what was shown immediately after save — confirming data consistency.

## Pass/Fail Criteria

**Pass:**
- Flow view shows the updated data immediately after Save without requiring canvas reopen
- YAML view shows the updated data immediately after Save without requiring canvas reopen
- Both views are consistent with each other and with the saved state

**Fail:**
- Flow or YAML view continues to display outdated data after Save
- Updated data only appears after closing and reopening the canvas
- Flow and YAML views are inconsistent with each other after Save
