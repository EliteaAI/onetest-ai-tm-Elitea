---
id: ELITEA-4697
title: "Select Node Type List — Entry Points, Content, Layout and Dismissal"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7154, EliteaAI/elitea_issues#7156]
---
# ELITEA-4697: Select Node Type List — Entry Points, Content, Layout and Dismissal

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Select node type" list opens identically from every entry point, lists exactly the 10 current node types with the correct descriptions in a two-column grid, excludes deprecated types, and closes correctly.

**Coverage:**
- Entry points: **+ Add Node** (empty card), **+ Node** (toolbar), **+ Create new node** (line-release Dropdown)
- Two-column grid, icon + name + one-line description
- Exact descriptions for all 10 types
- Deprecated types excluded
- Dismissal: selection, outside click, Esc; no stacked panels
- Adding each of the 10 types; entry point and left-panel auto-collapse

## Preconditions

- Logged in to {{base_url}}
- A new, empty pipeline is open

## Test Data

| Type | Expected description |
|------|----------------------|
| Agent | Executes tasks using predefined goals, tools, and logic. |
| Code | Runs custom code to process or transform data. |
| Decision | Evaluates conditions and selects the next step. |
| Human-in-the-loop | Pauses flow for human input or approval. |
| LLM | Generates or processes text using a language model. |
| MCP | Connects to external data or services via MCP protocol. |
| Printer | Outputs results for display, logging, or debugging. |
| Router | Directs flow to different paths based on conditions. |
| State modifier | Updates or enriches the pipeline state. |
| Toolkit | Provides access to a set of tools or actions. |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the **+ Add Node** button on the empty-state card. | "Select node type" list opens as a two-column grid of cards; each card shows an icon, name and one-line description. |
| 2 | Verify the list content against Test Data. | Exactly 10 types; descriptions match Test Data verbatim. |
| 3 | Verify no deprecated types are listed. | Function, Condition, Pipeline, Loop, Loop from tool, Tool and Custom are **not** listed. |
| 4 | Press **Esc**. | List closes; no node is created. |
| 5 | Open the list again, click outside it. | List closes; no node is created. |
| 6 | Click **+ Node** in the toolbar. | The same list opens with identical content. |
| 7 | With the list open via **+ Add Node**, click **+ Node** (toolbar); then click **+ Node** again. | First click closes the list; second click reopens it. No duplicate/stacked lists in either direction. |
| 8 | Select **Agent**. | List closes; Agent node is added as the **entry point** (Entrypoint badge); empty card disappears; End node **appears but is not connected**; left side panel auto-collapses and the canvas goes full view. |
| 9 | Observe the new node's placement. | Placed in the visible area; not overlapping End and not off-screen. |
| 10 | Using **+ Node**, add each of the remaining 9 types one by one. | Each type is added in the new compact card style, placed in the visible area without overlapping other nodes. |
| 11 | From any node, drag from **Output** and release on empty canvas → **+ Create new node**. | The same "Select node type" list (same two-column grid and 10 types) opens. Esc / outside click closes it without changes and removes the dangling line. |
| 12 | Compare icons against the Figma frame "Select node type". | Icons are visually distinct per type and match Figma. |

## Expected Final State

The node-type list is identical from all three entry points, shows exactly the 10 current types with correct descriptions, excludes deprecated types, dismisses cleanly, and every type can be added.

## Pass/Fail Criteria

**Pass:**
- Same list from all entry points; exactly 10 types; descriptions verbatim
- No deprecated types
- Esc / outside click / selection close the list; no stacking
- First node becomes the entry point, End appears unconnected, left panel collapses
- All 10 types can be added without overlaps

**Fail:**
- Any entry point shows different content or a legacy plain list
- A deprecated type is listed, or a type/description is missing or wrong
- Esc/outside click creates a node or leaves a dangling line
- Stacked/duplicate lists
