---
id: ELITEA-0864
title: "Pipeline Creation - UI and API"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_management.TestCreatePipeline.test_create_pipeline_via_ui
  - tests.ui.pipelines.test_pipeline_management.TestCreatePipeline.test_create_pipeline_required_fields_validation
  - tests.ui.pipelines.test_pipeline_management.TestPipelineDashboard.test_pipeline_created_via_api_visible_in_dashboard
tags: []
requirements: []
---
# ELITEA-0864: Pipeline Creation - UI and API

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can create pipelines via UI with field validation, and API-created pipelines are visible in dashboard.

## Preconditions

- User logged into Elitea
- Access to Pipelines dashboard

## Test Data

- URL: {{base_url}}
- Name: autotest_pipeline_<timestamp>

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Click 'Create Pipeline' button | Dialog opens with required fields |
| ? | Fill name and description, submit | Pipeline created, appears in list |
| ? | Create pipeline via API | Pipeline visible in dashboard |

## Expected Final State

Pipeline visible in dashboard

## Pass/Fail Criteria

**Pass:**
- Pipeline created via UI
- Validation prevents empty fields
- API pipelines visible

**Fail:**
- Creation fails
- Invalid data accepted
- API pipeline not visible
