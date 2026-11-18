---
id: ELITEA-4717
title: "Pipeline — Node YAML View: Validation and Invalid YAML Handling"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_node_yaml_view.test_node_yaml_view_validation_and_invalid_yaml
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/4192956f2f30261a3b906f374face7b7517ff008
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7158]
---

# ELITEA-4717: Pipeline — Node YAML View: Validation and Invalid YAML Handling

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the node YAML tab supports renaming via `id`, rejects duplicate and empty names and `type` changes with clear errors (Save disabled), blocks invalid YAML with an inline error and a Fix / Discard prompt, and that Find/Replace and Copy are scoped to the node.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- A saved pipeline exists with nodes "LLM 1" (LLM, entry point) → "Code 1" (Code) → End.

---

## Test Data

| Field | Value |
|-------|-------|
| New id | `LLM main` |
| Duplicate id | `Code 1` |
| New type | `code` |
| Invalid YAML | remove the colon after `input` (e.g. `input [messages]`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline; click "LLM 1"; switch the panel to "YAML" | Node YAML for "LLM 1" is shown |
| 2 | Change `id: LLM 1` to `id: LLM main` | The card title updates to "LLM main"; the panel Name shows "LLM main" |
| 3 | Change `id` to `Code 1` | Error below the editor: "The name has been used by other nodes, please input a new name!". The rename is not applied. "Save" is disabled |
| 4 | Clear the `id` value (`id: ''`) | Error: "Name is required". The card title stays unchanged (not blank). "Save" is disabled |
| 5 | Restore `id: LLM main`; change `type: llm` to `type: code` | Error: "Node type can't be changed in the node YAML.". The change is not applied. "Save" is disabled |
| 6 | Restore `type: llm`; break the syntax (remove the colon after `input`) | Inline error starting with "Invalid YAML:" is shown. "Save" is disabled |
| 7 | Switch the page toggle to "Yaml" and back to "Flow" | Page Yaml still contains the last valid "LLM main" block (invalid edit not applied) |
| 8 | In the panel click "Flow" (switch tabs) while the node YAML is invalid | Modal "Invalid node YAML" with text "The node YAML has errors, so it wasn't applied. Fix it, or discard your YAML changes to go back to the last valid version." and buttons "Fix" / "Discard YAML Changes" |
| 9 | Click "Fix" | Modal closes; the panel stays on YAML with the error still shown |
| 10 | Click the panel "✕" close button | The same "Invalid node YAML" modal appears |
| 11 | Click "Discard YAML Changes" | The node YAML reverts to the last valid version; the error disappears |
| 12 | Click in the node YAML editor and press Ctrl+F; search for `transition` | Find panel opens; matches are found only within this node's YAML |
| 13 | Press Ctrl+H | Replace panel opens (Replace / Replace all available) |
| 14 | Click the Copy icon (top-right of the editor) | Node YAML is copied to the clipboard; "Copied" confirmation is shown (soft) |

---

## Expected Final State

Invalid names, type changes and invalid YAML are never applied; Save is disabled while any error is shown; the Fix / Discard prompt protects against leaving with invalid YAML.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each validation shows the exact error, blocks the change and disables Save.
- Fix keeps the error; Discard YAML Changes reverts to the last valid YAML.

**Fail:**
- A duplicate/empty name, a type change or invalid YAML is applied to the pipeline.
- Save stays enabled while an error is shown.
- Switching tabs or closing the panel with invalid YAML does not show the prompt.
