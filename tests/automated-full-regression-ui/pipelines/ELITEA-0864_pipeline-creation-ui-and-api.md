---
id: ELITEA-0864
title: "Pipeline Creation - UI and API"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_management.TestCreatePipeline.test_create_pipeline_via_ui
  - tests.ui.pipelines_2.test_pipeline_management.TestCreatePipeline.test_create_pipeline_required_fields_validation
  - tests.ui.pipelines_2.test_pipeline_management.TestPipelineDashboard.test_pipeline_created_via_api_visible_in_dashboard
tags: []
requirements: []
---
# ELITEA-0864: Pipeline Creation - UI and API

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can create pipelines via the UI (the editor opens directly with a pre-filled default Name, and only the Name field gates Save), and that pipelines created via API are visible in the dashboard.

## Preconditions

- User is logged into Elitea and has access to the Pipelines dashboard
- Permission to create pipelines in the selected project
- For the API step: a valid API token for the same project

## Test Data

- URL: {{base_url}}
- Name: autotest_pipeline_<timestamp> (Name is limited to 32 characters)
- Description: Automated test pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipelines dashboard and click '+ Pipeline' | The pipeline editor opens directly (no dialog/modal) |
| 2 | Observe the Name field | Name is pre-filled with a non-empty default (e.g. "Pipeline N") |
| 3 | Observe the Description field and the Save button | Description is empty (optional); Save is enabled immediately |
| 4 | Clear the Name field completely | Save becomes disabled |
| 5 | Type a valid name (e.g. autotest_partial) | Save becomes enabled again |
| 6 | Leave Description empty throughout steps 2-5 | Description never affects Save; Save state tracks the Name field only |
| 7 | Enter a unique Name and a Description, then click Save | Pipeline is created; the pipeline detail page opens showing the saved Name |
| 8 | Open the Pipelines dashboard | The created pipeline appears in the list |
| 9 | Create a pipeline via the API (POST to the pipelines/applications endpoint with a unique name) | API responds successfully and returns the new pipeline id |
| 10 | Refresh the Pipelines dashboard | The API-created pipeline is visible in the dashboard |

## Expected Final State

Both the UI-created and the API-created pipelines are visible in the dashboard.

## Pass/Fail Criteria

**Pass:**
- Pipeline editor opens directly from '+ Pipeline' with a pre-filled default Name and Save enabled
- Clearing Name disables Save; entering a valid name re-enables it
- An empty Description never disables Save
- Pipeline created via UI appears in the list with the saved Name
- API-created pipeline is visible in the dashboard

**Fail:**
- A dialog/modal is shown instead of the editor, or Name is empty by default
- Save stays enabled with an empty Name, or stays disabled with a valid Name
- Save state depends on the Description
- UI creation fails or the saved Name is not shown
- API-created pipeline is not visible in the dashboard
