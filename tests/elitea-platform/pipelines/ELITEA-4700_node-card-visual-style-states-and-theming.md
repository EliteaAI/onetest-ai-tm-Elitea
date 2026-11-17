---
id: ELITEA-4700
title: "Node Card — Visual Structure, States, End Node and Theming"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7156]
---
# ELITEA-4700: Node Card — Visual Structure, States, End Node and Theming

**Module:** Pipelines · **Priority:** Medium · **Type:** UI

**Objective:** Verify the new compact node card structure, its Default/Hover/Selected states, the End node pill, edge labels and deprecated badges, in both dark and light themes, across all node types.

**Coverage:**
- Card header (type icon tile, name, muted type), Entrypoint badge, Input/Output pills, ＋ under Output
- Decision/Router extra Default output pill
- Default / Hover / Selected states
- End node compact pill
- Deprecated badge on legacy node types
- Edge labels (e.g. Interrupt)
- Dark and light theme
- Manual only (visual)

## Preconditions

- Logged in to {{base_url}}
- A pipeline containing all 10 node types
- An existing pipeline with a deprecated node (e.g. Condition or Function) and an interrupt edge

## Test Data

- Figma frames: "Node card", "Cards States & Statuses"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe each card header. | Type icon tile, **node name** (line 1), **node type** muted (line 2). |
| 2 | Observe the entry-point node. | Blue **Entrypoint** pill in its header; no other card has it. |
| 3 | Observe pills on every card. | **Input** pill on top; **Output** pill at the bottom with a **＋** under it. Decision and Router also show a **Default output** pill with ＋. |
| 4 | Observe a card at rest, on hover, and when selected. | Default: dark surface, subtle border. Hover: lighter border/surface. Selected: cyan border with glow. |
| 5 | Observe the End node. | Compact pill: flag icon + "End" text (not the old card shape). |
| 6 | Repeat steps 1–4 for every node type. | Structure is identical across types; only the body colour varies per type. |
| 7 | Open the existing pipeline with a deprecated node. | Header shows the orange **Deprecated!** pill; body shows "⚠ Deprecated"; rendered in the new card style. |
| 8 | Observe an edge with an interrupt. | **Interrupt** label renders cleanly on the edge. |
| 9 | Switch to light theme; repeat steps 1–8. | All card styles and states render correctly in light theme. |
| 10 | Compare against the Figma frames. | Layout matches. Note: actual cards use a per-type body colour vs. Figma's uniform dark body (logged, accepted). |

## Expected Final State

All node cards use the new compact structure and correct states in both themes; End, deprecated badges and edge labels render correctly.

## Pass/Fail Criteria

**Pass:**
- Card structure and pills as described on every type
- Default/Hover/Selected states distinguishable and as specified
- End pill, deprecated badge and edge labels render correctly
- Both themes render correctly

**Fail:**
- Any type renders in the old large card style
- Missing pills/badge, or Entrypoint badge on a non-entry node
- States indistinguishable or broken in either theme
