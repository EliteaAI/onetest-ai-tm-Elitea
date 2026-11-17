---
id: ELITEA-2060
title: "Pipeline — Node Deletion via Node Panel Footer"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157]
automation_test_id:
  - tests.ui.pipelines.test_pipeline_canvas_delete_node.test_delete_middle_node_removes_its_edges_and_persists
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/d23d9238a2b1c684f7ccd7451ea6ace1e57f18af
---

# ELITEA-2060: Pipeline — Node Deletion via Node Panel Footer

> **Updated for Pipelines 2.0:** node cards are view-only (#7157) — deletion is done only via the Delete icon in the node configuration panel footer; title and objective updated.

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a node can be deleted using the Delete icon in the node configuration panel footer (node cards are view-only), and that the node and all connected edges are removed with the Save button becoming enabled.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with multiple connected nodes exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with multiple nodes | Pipeline canvas is displayed with multiple nodes |
| 2 | Click a non-entry-point node on the canvas | Node is selected and its configuration side panel opens |
| 3 | Locate the "Delete node" button in the side panel footer | Delete button is visible in the panel footer |
| 4 | Click "Delete node" and confirm the "Are you sure to delete this node" dialog | Node deletion is triggered |
| 5 | Verify node is removed from canvas | Node no longer appears on the canvas |
| 6 | Verify edges to/from that node are removed | All edges connected to the deleted node are gone |
| 7 | Verify "Save" button becomes enabled | Save button is active indicating unsaved changes |

---

## Expected Final State

The node and all its connected edges are removed from the canvas via the side panel's Delete node button. The Save button becomes enabled to reflect the unsaved change.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Node and edges are removed; Save button becomes enabled.

**Fail:**
- Any step produces an error or unexpected result.
- Node is not deleted, edges remain, or Save button does not become enabled.
