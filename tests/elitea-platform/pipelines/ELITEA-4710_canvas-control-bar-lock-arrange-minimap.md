---
id: ELITEA-4710
title: "Canvas Control Bar — Tooltips, Lock/Unlock, Arrange Menu and Minimap"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7160]
---
# ELITEA-4710: Canvas Control Bar — Tooltips, Lock/Unlock, Arrange Menu and Minimap

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the canvas control bar (order and tooltips), Lock/Unlock behaviour, Arrange top-to-bottom / left-to-right with persistence and Discard, and the Minimap (show/hide, pan, sync with selection and zoom).

**Coverage:**
- 6 controls in order with exact tooltips; no card-density toggle
- Fit view idempotent
- Locked: no drag/connect/create; zoom/pan still work; Unlock restores
- Arrange menu ✓ on active orientation; TB/LR layouts; pills switch sides in LR
- Arrange + Save persists after reload; Discard restores; new node placement; existing pipelines not auto-arranged
- Minimap: bottom right, viewport frame, click/drag pans, zoom reflected, selection highlighted, visibility remembered
- Edge click highlights the edge

## Preconditions

- Logged in to {{base_url}}
- A pipeline with Router/Decision branches and 8+ nodes

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe the control bar. | Exactly 6 controls in order: Zoom in, Zoom out, Fit view, Lock/Unlock, Arrange, Minimap. No "Card density" / "Toggle cards size" control. |
| 2 | Hover each control. | *"Zoom in"*, *"Zoom out"*, *"Fit view"*, *"Lock canvas"* (when unlocked) / *"Unlock canvas"* (when locked), *"Auto-arrange"*, *"Show minimap"* / *"Hide minimap"*. |
| 3 | Zoom in/out, then click **Fit view** twice. | Whole pipeline fits into view; second click changes nothing. |
| 4 | Click **Lock**. | Icon changes to locked. Nodes can't be dragged; ＋ Output is not shown on hover (no connect/create); zoom and pan still work. |
| 5 | Click **Unlock**. | Drag, connect and create from handles work again. |
| 6 | Click **Arrange**. | Menu with **Arrange top to bottom** and **Arrange left to right**; ✓ on the active orientation. |
| 7 | Choose **Arrange top to bottom**. | Entry point at the top, flow downward, no overlapping cards/labels, view auto-fits; branch order preserved; Save enabled. |
| 8 | Choose **Arrange left to right**. | Entry point at the left, flow rightward, Input pills on the left and Output pills on the right, no overlaps. |
| 9 | Click **Discard**. | Previous (pre-arrange) layout restored. |
| 10 | Arrange, Save, reload. | Same orientation and positions after reload; ✓ shows that orientation. |
| 11 | Add a new node after arranging; run Arrange again. | New node is placed in free space and then incorporated into the layout. |
| 12 | Open an existing pipeline. | Saved positions/orientation shown; Arrange not auto-triggered. |
| 13 | Click **Minimap**. | Minimap appears bottom right with a viewport frame. |
| 14 | Click and drag inside the minimap. | Main canvas pans accordingly. |
| 15 | Zoom in/out on the canvas; select a node. | Viewport frame resizes; selected node highlighted in the minimap. |
| 16 | Reload. | Minimap visibility choice is remembered. |
| 17 | Click an edge. | The edge is highlighted. |

## Expected Final State

The control bar exposes the 6 controls with correct tooltips; Lock blocks editing only; Arrange lays out and persists correctly; the minimap navigates and stays in sync.

## Pass/Fail Criteria

**Pass:**
- Order, tooltips and absence of density toggle as specified
- Lock blocks drag/connect/create, keeps zoom/pan
- Arrange TB/LR correct, persists, Discard restores, not auto-applied
- Minimap shows, pans, syncs and is remembered

**Fail:**
- Missing/extra control or wrong tooltip
- Editing possible while locked
- Arrange overlaps, does not persist, or is auto-applied on open
- Minimap does not pan or sync
