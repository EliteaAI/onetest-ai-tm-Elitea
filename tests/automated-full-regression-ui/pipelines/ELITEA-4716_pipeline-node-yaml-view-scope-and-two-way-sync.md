---
id: ELITEA-4716
title: "Pipeline — Node YAML View: Scope and Two-Way Sync"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7158]
---

# ELITEA-4716: Pipeline — Node YAML View: Scope and Two-Way Sync

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the YAML tab of the node configuration panel shows only the selected node's YAML block, that it matches the same block in the page-level Yaml tab, that edits sync both ways (node YAML ↔ Flow fields, card summary, canvas edges, page Yaml), and that unknown keys are preserved.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- A saved pipeline exists: "LLM 1" (LLM, entry point) → "Printer 1" (Printer) → End, plus a "Code 1" (Code) node connected to End. The pipeline YAML contains `interrupt_before: [Printer 1]` at pipeline level.

---

## Test Data

| Field | Value |
|-------|-------|
| New task value | `Summarize the input` |
| New transition | `Code 1` |
| Flow field edit | LLM 1 System = `You are a helpful assistant` |
| Unknown key | `custom_note: keep_me` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline; click the "LLM 1" card; in the panel header switch from "Flow" to "YAML" (code icon) | The node YAML editor opens inside the panel |
| 2 | Inspect the node YAML content | Only the "LLM 1" node block is shown (id, type, input, input_mapping, output, transition, …). No `state`, `entry_point`, `interrupt_before` / `interrupt_after` keys and no other nodes are present |
| 3 | Switch the page-level toggle (top of canvas) from "Flow" to "Yaml"; locate the "LLM 1" block in the `nodes` list | The "LLM 1" block in the page Yaml is identical to the node YAML from step 2 |
| 4 | Switch the page back to "Flow"; in the "LLM 1" node YAML change the task value to `Summarize the input`; stop typing | After a short debounce: the panel's Flow view Task field shows `Summarize the input`; the "LLM 1" card summary updates; "Save" becomes enabled |
| 5 | Switch the page toggle to "Yaml" | The page Yaml "LLM 1" block contains the new task value |
| 6 | Switch back to "Flow"; in the "LLM 1" node YAML change `transition` from `Printer 1` to `Code 1` | The canvas edge from "LLM 1" now goes to "Code 1" instead of "Printer 1"; the page Yaml shows `transition: Code 1` |
| 7 | In the "LLM 1" panel switch to "Flow"; set System to `You are a helpful assistant`; switch to "YAML" | The node YAML shows the new System value |
| 8 | On the canvas, drag a new edge from "LLM 1" Output to "Printer 1" | The "LLM 1" node YAML `transition` updates to `Printer 1` |
| 9 | In the "LLM 1" node YAML add a new line `custom_note: keep_me`; click "Save"; reload the page; open "LLM 1" → "YAML" | The node YAML still contains `custom_note: keep_me` |

---

## Expected Final State

The node YAML tab is scoped to one node, matches the page Yaml, and stays in sync in both directions; unknown keys survive save and reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Node YAML shows only its node block and matches the page Yaml.
- Every edit propagates to Flow fields, card summary, canvas edges and page Yaml; the unknown key persists.

**Fail:**
- Node YAML includes other nodes or pipeline-level keys.
- Any edit does not propagate, or the unknown key is stripped.

**Notes:** Renaming a node does not update other nodes' references — enhancement EliteaAI/elitea_issues#7408, out of scope for this case.
