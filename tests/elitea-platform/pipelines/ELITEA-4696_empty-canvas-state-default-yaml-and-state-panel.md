---
id: ELITEA-4696
title: "Empty Canvas — Empty State, Default YAML, State Panel and Canvas Controls"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7154]
---
# ELITEA-4696: Empty Canvas — Empty State, Default YAML, State Panel and Canvas Controls

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the empty-state card, default YAML scaffold, State panel defaults and canvas controls on a brand-new pipeline with zero nodes, and that the empty state returns correctly after all nodes are deleted and after reopening.

**Coverage:**
- Empty-state card text and **+ Add Node** button
- End node not rendered while there are zero nodes
- Default YAML scaffold
- State panel default toggles
- Canvas controls available; Auto-arrange disabled
- Empty state after deleting nodes (one by one) and after save/reopen
- Test Pipeline disabled on the empty canvas
- See ELITEA-4714 for the main add-first-node flow

## Preconditions

- Logged in to {{base_url}}

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click **+ Pipeline**. Observe the canvas (Flow is selected by default). | Empty-state card: *"Start by adding your first node to the canvas!"* with a **+ Add Node** button. No End node is rendered. |
| 2 | Observe the canvas controls (bottom left). | Zoom in, Zoom out, Fit view, Lock, Auto-arrange, Minimap are present. **Auto-arrange is disabled** (no nodes). |
| 3 | Observe the **Test Pipeline** button; hover and click it. | Disabled. Tooltip/message: *"Save the pipeline to test it."* No panel opens. |
| 4 | Observe the **+ Node** toolbar button. | Present and enabled. |
| 5 | Click **State** (top right of canvas). | STATE panel: `input` toggle ON, `messages` toggle ON, `tool_outcomes` toggle OFF, `last_tool_outcome` toggle OFF. |
| 6 | Switch to the **Yaml** tab. | Default content: `state:` / `input: type: str` / `messages: type: list`. Copy and full-screen icons at top right. No **+ Node** button in Yaml view. |
| 7 | Switch back to Flow. Save the pipeline with zero nodes. Reopen it. | Reopens correctly in the empty state (empty card shown, no End node). |
| 8 | Add three nodes. Delete them one by one. | The empty-state card appears only after the **last** node is removed. |
| 9 | After the last node is deleted, observe End and Test Pipeline. | End is hidden again. Test Pipeline is disabled again. |
| 10 | Add a node, Save, delete the node, Save again, reopen. | Reopens in the correct empty state — no stale End node. |
| 11 | Open an existing pipeline (created before this release). | Opens normally with its nodes — not forced into the empty state. |

## Expected Final State

A pipeline with zero nodes always shows the empty-state card with + Add Node, no End node, disabled Test Pipeline and Auto-arrange, and the default YAML/State scaffold — both on first open and after deleting all nodes or reopening.

## Pass/Fail Criteria

**Pass:**
- Empty-state text and + Add Node button shown exactly as specified
- End hidden and Test Pipeline disabled whenever there are zero nodes
- Default YAML and State toggles match the expected scaffold
- Empty state survives save/reopen and re-appears only after the last node is deleted

**Fail:**
- End node rendered on an empty canvas
- Empty state appears while nodes still exist, or doesn't return after deleting all nodes
- Stale End node after save/reopen
- Default YAML or State toggles differ from the expected scaffold
