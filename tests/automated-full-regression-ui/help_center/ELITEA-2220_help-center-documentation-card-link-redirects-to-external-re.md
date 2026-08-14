---
id: ELITEA-2220
title: "Help Center — Documentation card link redirects to external resource"
priority: medium
type: functional
module: help-center
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:help-center]
requirements: []
automation_test_id:
  - tests.ui.help_center.test_help_center_resource_links.TestHelpCenterResourceLinks.test_resource_card_link_redirects_to_external_page[ELITEA-2220-documentation-getting-started]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1493
---

# ELITEA-2220: Help Center — Documentation card link redirects to external resource

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Documentation card link redirects to external resource. Success is confirmed when verify the target page loads without errors.

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
| 2 | Locate the DOCUMENTATION card (blue icon, subtitle: "API reference, guides, and platform concepts") | Action completes without error and produces the expected UI state. |
| 3 | Verify links displayed: Getting Started, How-To Guides, Integrations, Migration & Update | Condition holds as described. |
| 4 | Click the "Getting Started" link | Control responds; expected next state is shown. |
| 5 | Verify the user is redirected to the relevant documentation page in a new tab or window | Condition holds as described. |
| 6 | Verify the target page loads without errors | Condition holds as described. |

---

## Expected Final State

Verify the target page loads without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Documentation card link redirects to external resource.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
