---
id: ELITEA-4708
title: "Node YAML View — Scope, Editor Capabilities and Two-way Sync"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7158]
---
# ELITEA-4708: Node YAML View — Scope, Editor Capabilities and Two-way Sync

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the node panel's YAML tab shows only that node's YAML (identical to its block in the page Yaml tab), provides the standard editor features scoped to the node, syncs both ways with Flow view, the card, edges and the page Yaml, and keeps unknown keys — for every node type.

**Coverage:**
- Node-scoped content; no pipeline-level keys
- Identical to the node's block in the page Yaml tab — all 10 types
- Header, Name and footer unchanged in YAML view
- Syntax highlighting, line numbers, folding
- Ctrl/Cmd+F, Ctrl/Cmd+H scoped to the node; Copy icon
- YAML → Flow / card / edges / page Yaml; Save enabled
- Flow → YAML; canvas connection → YAML
- Unknown keys preserved
- Opening/closing without edits changes nothing
- See ELITEA-4716 for the main flow

## Preconditions

- Logged in to {{base_url}}
- A pipeline with all 10 node types and pipeline-level `interrupt_before` set

## Test Data

- Unknown key: `my_custom_key: test`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any node's panel and click the **YAML** (code icon) toggle. | Only this node's block is shown; no `state`, `entry_point` or `interrupt_before/after`. Header, Name and footer stay the same as in Flow view. |
| 2 | For each of the 10 node types, compare the node YAML with that node's block in the page **Yaml** tab. | Identical for every type, including multi-line templates/code and nested `input_mapping`. |
| 3 | Observe the editor. | Line numbers, fold arrows on multi-line keys, YAML syntax colouring. |
| 4 | Press Ctrl/Cmd+F and search a value present in other nodes too. | Find opens with next/previous/all, match case, regexp, by word; matches are only within this node's YAML. |
| 5 | Press Ctrl/Cmd+H; replace a value. | Replace / Replace all work within this node only. |
| 6 | Click the Copy icon (top right) and paste elsewhere. | This node's YAML is copied. |
| 7 | Edit `task` (or `template`) in the node YAML and stop typing. | After a short debounce the Flow field, the card summary and the page Yaml update; Save becomes enabled. |
| 8 | Change `transition` to another node. | The edge on the canvas moves to that node. |
| 9 | Switch to Flow; edit a field; switch back to YAML. | Node YAML reflects the change. |
| 10 | Connect the node to a different node on the canvas. | Node YAML `transition` updates. |
| 11 | Add `my_custom_key: test` in the node YAML; Save; reload. | The key is kept. |
| 12 | Open and close the YAML tab on a node without editing. | Save stays disabled; YAML unchanged. |

## Expected Final State

The node YAML tab is a correctly scoped, fully synced editor for a single node, identical to the page Yaml for that node, with node-scoped Find/Replace/Copy and unknown keys preserved.

## Pass/Fail Criteria

**Pass:**
- Node-only content identical to the page Yaml block, for all types
- Editor features present and scoped to the node
- Two-way sync with Flow, card, edges and page Yaml
- Unknown keys kept; no-op open/close changes nothing

**Fail:**
- Pipeline-level keys or other nodes appear
- Drift between node YAML and page Yaml
- Sync missing in any direction
- Unknown keys stripped
