---
id: ELITEA-2068
title: "Pipeline — YAML Editor Invalid Syntax"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_yaml_editor_invalid_syntax.test_yaml_editor_invalid_syntax_blocks_save
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1160
---

# ELITEA-2068: Pipeline — YAML Editor Invalid Syntax

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the pipeline cannot be saved with invalid YAML syntax and that an appropriate error message is shown.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing pipeline is open.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline and switch to "Yaml" view | YAML editor is displayed |
| 2 | Introduce invalid YAML syntax (e.g., remove a colon, add random text) | YAML content contains invalid syntax |
| 3 | Switch to "Flow" view | Flow view is displayed (may show partial or error state) |
| 4 | Verify the save button is enabled (indicating unsaved changes) | Save button is active |
| 5 | Attempt to save the pipeline — verify an error message appears indicating invalid YAML | Error message is shown; save is blocked |
| 6 | Verify pipeline cannot be saved with invalid YAML (or Save shows error) | Pipeline save operation fails with an error indicating invalid YAML |

---

## Expected Final State

The pipeline save operation fails gracefully when YAML contains invalid syntax, and an appropriate error message is displayed to the user. The pipeline is not saved with invalid YAML.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Invalid YAML blocks the save operation and an error message is displayed.

**Fail:**
- Any step produces an unexpected result.
- Pipeline saves with invalid YAML without error, or no error message appears.
