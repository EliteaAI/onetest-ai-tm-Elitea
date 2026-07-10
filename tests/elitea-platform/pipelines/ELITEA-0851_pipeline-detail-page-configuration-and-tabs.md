---
id: ELITEA-0851
title: "Pipeline Detail Page - Configuration and Tabs"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_management.TestEditPipeline.test_pipeline_detail_page_loads
  - tests.ui.pipelines.test_pipeline_management.TestEditPipeline.test_pipeline_has_configuration_and_history_tabs
tags: []
requirements: []
---
# ELITEA-0851: Pipeline Detail Page - Configuration and Tabs

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify pipeline detail page loads correctly and displays configuration and history tabs.

**Coverage:**
- Pipeline detail page loads successfully
- Pipeline has Configuration and History tabs

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Expected tabs: Configuration, History

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Open any existing pipeline to view its detail page. | The pipeline detail page loads within 15 seconds. The pipeline name and description are visible. |
| 2 | Verify the pipeline name displayed on the detail page matches the expected name. | The displayed name matches the pipeline name from the dashboard. |
| 3 | Verify the pipeline description is displayed correctly. | The description matches what was set when the pipeline was created. |
| 4 | Look at the tab bar near the top. Verify a 'Configuration' tab is present. | The Configuration tab is visible. |
| 5 | Verify a 'History' tab is also present and clickable. | The History tab is visible. Clicking it shows version history content. |

## Expected Final State

The History tab is visible. Clicking it shows version history content.

## Pass/Fail Criteria

**Pass:**
- Detail page loads with correct name and description
- Both Configuration and History tabs visible
- Tab content accessible via click

**Fail:**
- Detail page fails to load or shows wrong pipeline
- Name or description mismatch
- Configuration or History tab missing
