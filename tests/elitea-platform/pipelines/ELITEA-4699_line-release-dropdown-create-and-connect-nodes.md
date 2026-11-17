---
id: ELITEA-4699
title: "Line-release Dropdown — Create or Connect Nodes from an Output Handle"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7156]
---
# ELITEA-4699: Line-release Dropdown — Create or Connect Nodes from an Output Handle

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the line-release Dropdown that opens when a connection line is released on empty canvas (or the + under Output is clicked): it lists **+ Create new node** and existing nodes, creates and auto-connects new nodes at the release point, connects to existing nodes, and dismisses cleanly.

**Coverage:**
- Opening by drag-release and by the + under Output
- Dropdown content: + Create new node, existing nodes (icon + name, excluding source), End when unconnected
- Empty message "No other nodes created yet"
- Create new node → same node-type list → created at release point and connected
- Select existing node → connects only
- Esc / outside click → no changes, dangling line removed
- All 10 types via this path; chained creation

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with one configured node (entry point) not yet connected to End

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Drag a line from the node's **Output** handle and release on empty canvas. | A Dropdown opens at the release point. |
| 2 | Observe the Dropdown content. | **＋ Create new node** is the first item; below it the existing nodes (type icon + name), excluding the source node. **End** is listed while it is not yet connected. |
| 3 | Press **Esc**. | Dropdown closes; no node or edge created; dangling line removed. |
| 4 | Click the **＋** under the node's Output (no drag). | The same Dropdown opens. Click outside → closes with no changes. |
| 5 | Open the Dropdown and select **End**. | The line connects to End; no new node is created. |
| 6 | With End connected and no other nodes, open the Dropdown. | Muted message *"No other nodes created yet"* is shown instead of a list. |
| 7 | Select **＋ Create new node**. | The same "Select node type" two-column list opens (same 10 types). |
| 8 | In that list press Esc. | Closes without changes; dangling line removed. |
| 9 | Open again → **＋ Create new node** → pick **LLM**. | LLM node is created at the release point and automatically connected from the source node. |
| 10 | Repeat step 9 for each of the 10 node types. | Each type is created at the release point, connected, and rendered in the new card style. |
| 11 | Build a 4-node linear chain entirely via Output → Dropdown → Create new node. | No edge or positioning glitches accumulate. |
| 12 | Drag a line from Output and release it directly **on top of** an existing node. | Connects directly to that node; no Dropdown opens. |
| 13 | Open the Dropdown from one node, then open it from another node's Output without resolving the first. | Only one Dropdown is open; no stacking. |
| 14 | Lock the canvas (Lock control) and hover a node. | The ＋ Output control is not shown; the Dropdown cannot be opened. |

## Expected Final State

The line-release Dropdown reliably creates and auto-connects any node type at the release point or connects to an existing node, and dismisses without side effects.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens from drag-release and from the + under Output
- Correct content and empty message
- New nodes created at the release point and auto-connected, for all 10 types
- Esc / outside click leaves no node, edge or dangling line
- Blocked while the canvas is locked

**Fail:**
- Dropdown missing or showing a legacy list
- Node not connected or placed away from the release point
- Dangling line remains after dismissal; stacked dropdowns
