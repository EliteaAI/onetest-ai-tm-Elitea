---
id: ELITEA-4711
title: "Canvas — Saved Positions, Compact View Below 60%, Zoom Limits and Left Panel Auto-collapse"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7160]
---
# ELITEA-4711: Canvas — Saved Positions, Compact View Below 60%, Zoom Limits and Left Panel Auto-collapse

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that manual node positions are saved exactly as shown, cards switch to compact view below 60% zoom, zoom limits/steps are respected, the left settings panel auto-collapses on node interaction, and an unchanged existing pipeline keeps Save disabled.

**Coverage:**
- Manual drag → Save enabled → positions kept after reload; Discard restores
- Mixed drag + Arrange; final saved layout = last shown
- Compact (header-only) cards below 60%; normal above; selection/run state/Entrypoint visible when compact
- Zoom min 10%, max 200%, step size
- Left panel auto-collapses on select/drag/connect/+ Node; re-expands only via its own button
- Manual only (hard to assert automatically)

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with 5+ nodes

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Drag nodes to new positions. | Save becomes enabled. |
| 2 | Click **Discard**. | Pre-drag positions restored. |
| 3 | Drag nodes again; Save; reload. | Nodes stay exactly where they were dragged (not auto-rearranged). |
| 4 | Drag → Save → Arrange → Discard → Arrange → Save → reload. | Discard returns to the dragged layout; final saved layout matches what was last shown. |
| 5 | Zoom out below 60%. | All cards render compact (header only). |
| 6 | Zoom back to 60% or above. | Normal cards with summary return. |
| 7 | Below 60%: select a node, run the pipeline, observe the entry node. | Selection, run-state highlight and Entrypoint badge remain visible on compact cards. |
| 8 | Click Zoom out until it stops; then Zoom in until it stops; count clicks. | Minimum ≈10%, maximum ≈200%; record the step size (spec ~20% per click; observed ~11% — needs confirmation). |
| 9 | With the left General panel expanded: select a node; expand again; drag a node; expand again; connect nodes; expand again; click **+ Node**. | The left panel auto-collapses on each interaction. |
| 10 | Observe how to re-expand it. | Only via its own `<<` / `>>` button, never automatically. |
| 11 | Open an existing pipeline and make no changes. | Save stays disabled. |

## Expected Final State

Manual positions persist exactly, compact view applies below 60% with key indicators visible, zoom stays within limits, and the left panel collapses on node interaction.

## Pass/Fail Criteria

**Pass:**
- Positions saved as shown; Discard restores
- Compact view threshold works and keeps selection/run state/Entrypoint visible
- Zoom bounded 10–200%
- Left panel auto-collapses and re-expands only manually

**Fail:**
- Save auto-rearranges or loses manual positions
- Compact view missing or hides key indicators
- Zoom exceeds limits
- Left panel does not collapse, or re-expands on its own
