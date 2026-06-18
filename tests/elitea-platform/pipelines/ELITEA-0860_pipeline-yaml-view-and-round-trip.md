---
id: ELITEA-0860
title: "Pipeline YAML View and Round-Trip"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_pipeline_advanced.py:TestYamlEditor.test_yaml_view_toggle
test_pipeline_advanced.py:TestYamlEditor.test_yaml_content_reflects_pipeline
test_pipeline_advanced.py:TestYamlEditor.test_flow_yaml_round_trip
test_pipeline_advanced.py:TestDiscardChanges.test_discard_reverts_name_change
tags: []
requirements: []
---
# ELITEA-0860: Pipeline YAML View and Round-Trip

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that pipelines support YAML view toggle, YAML content reflects pipeline structure, and flow/YAML round-trip works correctly.

**Coverage:**
- YAML view toggle button functional
- YAML content displays correct pipeline structure
- Flow → YAML → Flow round-trip preserves structure
- Discard button reverts unsaved changes

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists with an LLM node (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Expected YAML keywords when viewing pipeline: llm, entry_point, nodes
- Test name for discard: autotest_changed_name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Open an existing pipeline with at least one LLM node. Verify the Flow view (canvas) is active by default. | Pipeline canvas is visible showing nodes and connections in the Flow view. |
| 2 | Click the 'Yaml' toggle button (near the top of the canvas area) to switch to the YAML editor view. | A code editor appears showing the pipeline configuration in YAML format. |
| 3 | Read the YAML content in the editor. | YAML content is non-empty and contains pipeline structure keywords such as 'llm', 'entry_point', or 'nodes'. |
| 4 | Click the 'Flow' button to switch back to canvas view. Then toggle Flow > Yaml > Flow again to verify round-trip. | After switching back and forth, the same number of nodes are visible. No nodes are lost or duplicated. |
| 5 | Edit the pipeline name field: select all text in the name field, delete it, and type 'autotest_changed_name'. | The name field shows the updated value. |
| 6 | Click the 'Discard' button. In the warning dialog that appears, click 'Confirm'. | The page reloads within 15 seconds. The name field reverts to the original pipeline name. |

## Expected Final State

The page reloads within 15 seconds. The name field reverts to the original pipeline name.

## Pass/Fail Criteria

**Pass:**
- YAML view toggle works in both directions
- YAML content reflects pipeline structure with valid keywords
- Flow → YAML → Flow round-trip preserves node count
- Discard button reverts name to original value

**Fail:**
- YAML editor fails to render
- YAML content empty or missing pipeline keywords
- Round-trip loses or duplicates nodes
- Discard does not revert changes
