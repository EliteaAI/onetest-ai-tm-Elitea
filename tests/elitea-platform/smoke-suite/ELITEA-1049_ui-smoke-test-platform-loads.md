---
id: ELITEA-1049
title: "UI Smoke Test - Platform Loads"
priority: critical
type: functional
module: smoke-suite
status: ready
execution_type: automated
automation_test_id:
  - test_ui_smoke.py:test_page_loads
  - test_ui_smoke.py:test_main_content_visible
tags: []
requirements: []
---
# ELITEA-1049: UI Smoke Test - Platform Loads

**Module:** Smoke Suite · **Priority:** Critical · **Type:** Functional

**Objective:** Verify basic UI smoke test - platform loads and main pages are accessible.

**Coverage:**
- Landing page loads successfully
- After authentication, dashboard/main page loads

## Preconditions

- User is logged in to {{base_url}} via Keycloak (or login credentials are ready)
- Browser: Chrome or Chromium
- Network access to {{base_url}}

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a browser and navigate to {{base_url}} Log in if prompted. | The page loads successfully. The browser tab title shows a non-empty page title. |
| 2 | Verify the main content area is visible — the page should not show a blank screen or error page. | The main application content is visible within 15 seconds. No broken layout or blank screen. |

## Expected Final State

The main application content is visible within 15 seconds. No broken layout or blank screen.

## Pass/Fail Criteria

**Pass:**
- Page title is non-empty
- Main content area visible within 15 seconds
- No 5xx errors during page load

**Fail:**
- Page returns blank/empty title
- Main content not visible within 15 seconds
- 5xx server errors during load
- Page shows error screen
