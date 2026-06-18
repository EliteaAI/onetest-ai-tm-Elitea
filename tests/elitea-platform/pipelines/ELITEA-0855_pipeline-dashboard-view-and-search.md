---
id: ELITEA-0855
title: "Pipeline Dashboard - View and Search"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_pipeline_management.py:TestPipelineDashboard.test_pipeline_dashboard_loads
test_pipeline_management.py:TestPipelineDashboard.test_pipeline_created_via_api_visible_in_dashboard
test_pipeline_management.py:TestPipelineDashboard.test_view_toggle_table_and_card
test_pipeline_management.py:TestSearchPipeline.test_search_pipeline_by_name
test_pipeline_management.py:TestSearchPipeline.test_search_pipeline_no_results
tags: []
requirements: []
---
# ELITEA-0855: Pipeline Dashboard - View and Search

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify pipeline dashboard functionality: loading, view toggles, and search capabilities.

**Coverage:**
- Pipeline dashboard loads successfully
- Pipeline created via API visible in dashboard
- View toggle between table and card view
- Search pipeline by name returns matching results
- Search with no matches shows empty state

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Non-existent search term: zzzz_nonexistent_pipeline_12345

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar to open the Pipelines dashboard. | Dashboard loads with 'Pipelines' header and a search input visible. |
| 2 | Look through the pipeline list to verify at least one pipeline is visible. | At least one pipeline appears in the list. |
| 3 | Look for view toggle icons (table/card view) near the top of the dashboard. Click the table view icon. | The view switches to a table layout. |
| 4 | Click the card view icon to switch back. | The view switches back to card layout. The 'Pipelines' header remains visible. |
| 5 | Type a known pipeline name into the search input field. | The list filters to show only matching pipelines within 10 seconds. |
| 6 | Clear the search field and type 'zzzz_nonexistent_pipeline_12345'. | The list shows no results / empty state within a few seconds. |

## Expected Final State

The list shows no results / empty state within a few seconds.

## Pass/Fail Criteria

**Pass:**
- Dashboard loads with header and search
- API-created pipeline visible in dashboard
- View toggle switches between table and card
- Search finds matching pipeline
- No-results search shows empty state

**Fail:**
- Dashboard fails to load
- Pipeline missing from list after API creation
- View toggle non-functional
- Search times out or returns wrong results
