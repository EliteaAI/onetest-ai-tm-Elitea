---
id: ELITEA-2221
title: "Help Center — Release Notes card link redirects to release notes page"
priority: medium
type: functional
module: help-center
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:help-center]
requirements: []
automation_test_id:
  - tests.ui.help_center.test_help_center_resource_links.TestHelpCenterResourceLinks.test_resource_card_link_redirects_to_external_page[ELITEA-2221-release-notes-latest]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1493
---

# ELITEA-2221: Help Center — Release Notes card link redirects to release notes page

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Release Notes card link redirects to release notes page. Success is confirmed when verify the target page loads without errors.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Help Center | Target page/section loads successfully. |
| 2 | Locate the RELEASE NOTES card (orange icon, subtitle: "Product updates, improvements, and fixes") | Action completes without error and produces the expected UI state. |
| 3 | Verify links displayed according to current/recent release versions: (Release 2.0.2 (latest), Release 2.0.1, Release 2.0.0, Release 2.0.0B2) | Condition holds as described. |
| 4 | Click the latest release link e.g. "Release 2.0.2 (latest)" | Control responds; expected next state is shown. |
| 5 | Verify the user is redirected to the release notes page for version 2.0.2 | Condition holds as described. |
| 6 | Verify the target page loads without errors | Condition holds as described. |

---

## Expected Final State

Verify the target page loads without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Release Notes card link redirects to release notes page.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
