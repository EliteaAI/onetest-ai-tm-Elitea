---
id: ELITEA-0854
title: "Pipeline Fixture Data Lifecycle"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_pipeline_management.py:TestPipelineIsolation.test_fixture_creates_fresh_pipeline
test_pipeline_management.py:TestPipelineIsolation.test_fixture_cleanup_cycle
tags: []
requirements: []
---
# ELITEA-0854: Pipeline Fixture Data Lifecycle

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pytest fixture behavior for pipeline test data: fresh creation and cleanup.

**Coverage:**
- Fixture creates fresh pipeline for each test
- Fixture cleanup cycle (create → use → delete)

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Pipeline name prefix for testing: autotest_
- Cleanup cycle pipeline name: autotest_cleanup_pipe

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Click 'Create Pipeline' to create a new pipeline with a name starting with 'autotest_' (e.g., 'autotest_lifecycle_pipe'). | A new pipeline is created and appears on the Pipelines dashboard. |
| 2 | Open the newly created pipeline's detail page from the dashboard. | The detail page loads. The Name field displays the pipeline name starting with 'autotest_'. |
| 3 | Verify the pipeline canvas is visible with at least the default END node. | The canvas shows at least the END node. The pipeline is functional. |
| 4 | Create another pipeline named 'autotest_cleanup_pipe'. | Pipeline is created successfully. |
| 5 | Go back to the Pipelines dashboard. Search for 'autotest_cleanup_pipe' to verify it appears in the list. | The pipeline appears in the search results. |
| 6 | Delete the 'autotest_cleanup_pipe' pipeline (via three-dot menu > Delete pipeline, type name to confirm). Refresh the dashboard and search again. | The pipeline no longer appears in the dashboard after deletion and refresh. |

## Expected Final State

The pipeline no longer appears in the dashboard after deletion and refresh.

## Pass/Fail Criteria

**Pass:**
- Fixture creates pipeline with "autotest_" prefix
- Pipeline ID matches between fixture and UI/API
- Create → list → delete → verify cycle completes
- No orphaned test data after cleanup

**Fail:**
- Fixture fails to create pipeline
- Pipeline ID mismatch
- Delete does not remove pipeline from API list
- Orphaned pipelines remain after test
