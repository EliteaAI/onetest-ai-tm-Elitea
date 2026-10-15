---
id: ELITEA-1052
title: "Platform Availability & Basic Navigation"
priority: critical
type: functional
module: smoke-suite
status: ready
execution_type: automated
automation_test_id:
  - tests.api.test_api_health.TestAPIHealth.test_api_root_reachable
  - tests.api.test_api_health.TestAPIHealth.test_api_returns_json
  - tests.api.test_api_health.TestAuthenticatedAPI.test_list_agents
  - tests.ui.smoke.test_ui_smoke.TestHomePage.test_page_loads
  - tests.ui.smoke.test_ui_smoke.TestHomePage.test_main_content_visible
tags: []
requirements: []
---
# ELITEA-1052: Platform Availability & Basic Navigation

**Module:** Smoke Suite · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Elitea platform is accessible, pages load correctly, basic navigation works, and API endpoints respond.

## Preconditions

- Browser installed (Chrome/Chromium)
- Network access to stage.elitea.ai
- Valid test user credentials configured

## Test Data

- URL: {{base_url}}
- Test user: alita@elitea.ai
- Password: rokziJ-nuvzo4-hucmih
- API endpoint: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open browser and navigate to {{base_url}} | Home page loads within 5 seconds, page title is present |
| ? | Verify main content area is visible (check for main layout elements) | Main content area renders correctly, no broken layout |
| ? | Open browser developer console and check for errors | No critical JavaScript errors or 500 HTTP errors in console |
| ? | Login with test credentials (username: test user, password from .env.test) | Login successful, user redirected to dashboard/main interface |
| ? | Verify user dashboard/main interface loads after login | Dashboard loads within 5 seconds, user menu/avatar visible |
| ? | Check API health: Open {{base_url}} in new tab | API responds with HTTP status < 500 (200, 401, or similar), returns JSON content |

## Expected Final State

API responds with HTTP status < 500 (200, 401, or similar), returns JSON content

## Pass/Fail Criteria

**Pass:**
- All 6 test steps pass
- Page load time < 5 seconds
- API returns 200/401 (authenticated/not authenticated)
- No 5xx errors

**Fail:**
- Any 5xx errors
- Login fails
- Critical JavaScript errors in console
- Page load timeout (> 10 seconds)
