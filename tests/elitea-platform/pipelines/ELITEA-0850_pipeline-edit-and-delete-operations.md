---
id: ELITEA-0850
title: "Pipeline Edit and Delete Operations"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_pipeline_management.py:TestEditPipeline.test_edit_pipeline_name
  - test_pipeline_management.py:TestEditPipeline.test_edit_pipeline_description
  - test_pipeline_management.py:TestDeletePipeline.test_delete_pipeline_via_api
  - test_pipeline_management.py:TestDeletePipeline.test_delete_pipeline_via_ui_menu
tags: []
requirements: []
---
# ELITEA-0850: Pipeline Edit and Delete Operations

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify pipeline editing and deletion via UI menu and API.

**Coverage:**
- Edit pipeline name
- Edit pipeline description
- Delete pipeline via API
- Delete pipeline via UI menu

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create additional ones for delete testing)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- New pipeline name for edit test: autotest_renamed_pipe
- New description for edit test: Updated by automation
- Pipeline names for delete tests: autotest_delete_pipe_1, autotest_delete_pipe_2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing pipeline's detail page. Select all text in the Name field, delete it, and type 'autotest_renamed_pipe'. | The Name field shows the new value. The Save button becomes enabled. |
| 2 | Click Save. After it completes, reload the page and check the Name field. | The Name field shows 'autotest_renamed_pipe' after reload — the change persisted. |
| 3 | Edit the Description field similarly: select all, type 'Updated by automation'. Save and reload. | The Description field shows 'Updated by automation' after reload. |
| 4 | Create a new pipeline named 'autotest_delete_pipe_1'. Verify it appears in the Pipelines dashboard. Delete it using any method. Refresh the page. | The pipeline appears before deletion. After deletion and refresh, it is gone from the list. |
| 5 | Create another pipeline named 'autotest_delete_pipe_2'. Open its detail page. | The pipeline detail page loads. |
| 6 | Click the three-dot menu in the header. Select 'Delete pipeline'. In the confirmation dialog, type the pipeline name and click 'Delete'. | The pipeline is deleted. You are navigated back to the Pipelines dashboard. The pipeline no longer appears in the list. |

## Expected Final State

The pipeline is deleted. You are navigated back to the Pipelines dashboard. The pipeline no longer appears in the list.

## Pass/Fail Criteria

**Pass:**
- Name edit persists after save + reload
- Description edit persists after save + reload
- API delete removes pipeline from dashboard
- UI menu delete removes pipeline with type-to-confirm dialog

**Fail:**
- Edits revert after reload
- API delete doesn't remove from UI
- Delete dialog doesn't appear
- Type-to-confirm doesn't work
- Pipeline remains after deletion
