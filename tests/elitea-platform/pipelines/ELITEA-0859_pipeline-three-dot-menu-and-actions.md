---
id: ELITEA-0859
title: "Pipeline Three-Dot Menu and Actions"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_pipeline_advanced.py:TestActionsMenu.test_three_dot_menu_lists_items
test_pipeline_advanced.py:TestActionsMenu.test_export_pipeline_if_available
tags: []
requirements: []
---
# ELITEA-0859: Pipeline Three-Dot Menu and Actions

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that pipeline three-dot menu lists available actions and export functionality works if available.

**Coverage:**
- Three-dot menu button opens
- Menu lists expected items
- Export pipeline option (if available)

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Expected menu items: Delete pipeline, Export (if available)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Open any existing pipeline to view its detail page. Close any banner overlay if it appears. | Pipeline detail page loads with the canvas and header visible. |
| 2 | Click the three-dot menu button (vertical ellipsis icon) in the top-right area of the page header. | A dropdown menu opens with at least one menu item listed. |
| 3 | Verify the menu contains a 'Delete pipeline' option. | The 'Delete pipeline' option is visible in the menu. |
| 4 | Check if an 'Export' option is present in the same menu. | Export option may or may not be present (varies by configuration). |
| 5 | If 'Export' is available, click it. | A file download is triggered (no dialog appears). The pipeline is exported as a file. |

## Expected Final State

A file download is triggered (no dialog appears). The pipeline is exported as a file.

## Pass/Fail Criteria

**Pass:**
- Three-dot menu opens successfully
- Menu lists at least one item
- Delete-related item found in menu
- Export works if available (triggers download)

**Fail:**
- Three-dot menu fails to open
- Menu is empty (0 items)
- No Delete-related item in menu
- Export fails with error (if available)
