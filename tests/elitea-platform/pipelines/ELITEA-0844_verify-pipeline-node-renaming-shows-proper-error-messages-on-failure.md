---
id: ELITEA-0844
title: "Verify pipeline node renaming shows proper error messages on failure"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157, EliteaAI/elitea_issues#7158]
---
# ELITEA-0844: Verify pipeline node renaming shows proper error messages on failure

> **Updated for Pipelines 2.0:** Renaming is done in the node panel's Name field (cards are view-only, #7157) or via `id` in the node YAML (#7158), using the actual error texts. Other nodes' references are not updated after a rename (enhancement #7408), so connection checks only cover the renamed node's own edges.

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that invalid node rename operations (empty name, duplicate name, invalid characters) show clear error messages and block saving, and that a valid rename works and persists. Negative-test complement to the node-rename happy path.

## Preconditions

User logged into Elitea
A pipeline exists with at least two nodes (e.g., two LLM nodes: 'LLM 1' and 'LLM 2')

## Test Data

| Field | Value |
|-------|-------|
| Existing node names | `LLM 1`, `LLM 2` |
| Duplicate-name error | "The name has been used by other nodes, please input a new name!" |
| Empty-name error | "Name is required" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline detail page with multiple nodes | Pipeline editor loads showing at least two nodes (e.g., 'LLM 1' and 'LLM 2') |
| 2 | Click the 'LLM 1' card to open its panel | Node panel opens with the Name field showing 'LLM 1' |
| 3 | Clear the Name field | Inline error **"Name is required"** is shown. Save is disabled. The card keeps showing 'LLM 1' |
| 4 | Type the name of the other existing node ('LLM 2') | Error **"The name has been used by other nodes, please input a new name!"** is shown. Save is disabled. The node is not renamed |
| 5 | Verify the error message is displayed in a readable format (not raw JSON, not truncated, not overlapping UI elements) | Error message is an inline message under the field; fully readable and properly formatted |
| 6 | Try renaming the node with special characters that may be invalid (e.g., '/', '\', or excessively long names) | Appropriate error messages are shown for invalid characters or length violations, or the name is accepted — record actual behavior. Messages are clear and actionable |
| 7 | Repeat steps 3–4 in the node's **YAML** tab by editing `id` | Same errors ("Name is required" / "The name has been used by other nodes, please input a new name!") are shown below the YAML editor and Save is disabled |
| 8 | Successfully rename the node to a valid, unique name (e.g., 'My LLM Node') in the Name field | Node is renamed. No errors displayed. The card title updates |
| 9 | Verify the renamed node's own outgoing connection is preserved | The edge from the renamed node is intact. (Incoming references from other nodes are not auto-updated — enhancement #7408, out of scope) |
| 10 | Rename the node back to its original name ('LLM 1') | Node accepts the original name without duplicate error. Roundtrip rename works correctly |
| 11 | Save the pipeline after renaming, then refresh the page and verify the renamed node persists with its new name | After page refresh, the node retains its renamed value |
| 12 | Switch to the page Yaml view and verify the renamed node name is correctly reflected | YAML shows the renamed node `id` |

## Expected Final State

Invalid rename attempts show the documented errors and block Save; a valid rename persists after save and refresh and is shown in the YAML.

## Pass/Fail Criteria

PASS: "Name is required" and "The name has been used by other nodes, please input a new name!" are shown for empty/duplicate names in both the Name field and node YAML; Save is disabled while an error is shown; valid rename and roundtrip rename work; name persists after save/refresh; YAML reflects the new name
FAIL: Error messages missing or improperly displayed (raw JSON, truncated, overlapping), Save allowed with an invalid name, node left in inconsistent state, name lost on refresh, or YAML shows stale name
