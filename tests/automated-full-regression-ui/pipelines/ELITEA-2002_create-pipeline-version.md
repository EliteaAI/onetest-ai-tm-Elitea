---
id: ELITEA-2002
title: "Create Pipeline Version"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_create_version.test_create_pipeline_version_save_list_switch_preserves_canvas_state
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2325
---

# ELITEA-2002: Create Pipeline Version

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can save a named pipeline version, switch between versions, and that each version preserves its own distinct node configuration.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with access to the Pipelines feature.

---

## Test Data

| Field | Value |
|-------|-------|
| Version name | v1_test |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline with name and description via UI | Pipeline is created and saved successfully |
| 2 | Modify instructions in the pipeline (add an LLM node, configure it) | LLM node is added and configured on the canvas |
| 3 | Click "Save as Version" and provide version name "v1_test" | Version is saved with the provided name |
| 4 | Verify version "v1_test" appears in the version dropdown | "v1_test" is listed in the VERSION dropdown |
| 5 | Switch back to "base" version — verify original state is intact | Canvas shows original node topology without the LLM modifications |
| 6 | Switch to "v1_test" — verify modifications are present | Canvas shows the LLM node and its configuration as saved |

---

## Expected Final State

The pipeline has two versions: "base" (original state) and "v1_test" (with LLM node modifications). Switching between versions restores the respective canvas state correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Version "v1_test" is saved, appears in the dropdown, and correctly preserves the LLM node configuration when selected.

**Fail:**
- Any step produces an error or unexpected result.
- Version "v1_test" does not appear in the dropdown, or switching versions does not restore the correct canvas state.
