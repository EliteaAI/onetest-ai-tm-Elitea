---
id: ELITEA-0800
title: "Save Button Persists Flow Changes on Newly Created Pipeline"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4967]
---
# ELITEA-0800: Save Button Persists Flow Changes on Newly Created Pipeline

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the Save button on a newly created pipeline (after its initial creation) persists flow changes and suppresses the unsaved-changes navigation warning.

**Coverage:**
- Save button is functional after adding a node to a newly created pipeline
- Flow changes (e.g., added LLM node) are persisted after clicking Save
- No unsaved-changes modal appears when navigating away after a successful save
- Pipeline canvas reflects the saved state on reload

## Preconditions

- Logged in to {{base_url}}
- User has permission to create pipelines in the active project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines in the main menu → click + New Pipeline → fill in Name and Description → click Save | Pipeline is created and the flow editor page loads |
| 2 | Add a node to the flow canvas (e.g., drag an LLM Node from the node panel onto the canvas) | Node appears on the canvas; an unsaved-state indicator or dirty flag is visible |
| 3 | Click the Save button | Save action completes — the page refreshes or shows a success indicator; no error is displayed; no silent no-op |
| 4 | Navigate away from the pipeline (e.g., click another section in the sidebar) | No "There are unsaved changes. Are you sure you want to leave?" modal appears |
| 5 | Return to the pipeline configuration page | The LLM node added in step 2 is still present on the canvas |

## Expected Final State

The LLM node added in step 2 is still present on the canvas

## Pass/Fail Criteria

**Pass:**
- Save button triggers a save action (page refresh or success notification)
- Added node is persisted; visible on return to the pipeline
- Unsaved-changes modal does NOT appear when navigating away after saving

**Fail:**
- Save button does nothing (no feedback, no refresh, no notification)
- Unsaved-changes modal appears despite having clicked Save
- Flow changes are lost after navigating away and returning
