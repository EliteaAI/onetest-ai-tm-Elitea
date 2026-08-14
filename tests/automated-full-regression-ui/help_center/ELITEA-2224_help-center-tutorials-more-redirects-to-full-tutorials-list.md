---
id: ELITEA-2224
title: "Help Center — Tutorials \"More...\" redirects to full tutorials list"
priority: medium
type: functional
module: help-center
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:help-center]
requirements: []
automation_test_id:
  - tests.ui.help_center.test_help_center_resource_links.TestHelpCenterResourceLinks.test_resource_card_link_redirects_to_external_page[ELITEA-2224-tutorials-more]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1493
---

# ELITEA-2224: Help Center — Tutorials \"More...\" redirects to full tutorials list

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Tutorials "More..." redirects to full tutorials list. Success is confirmed when verify the page loads without errors and displays more tutorials than shown in the card preview.

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
| 2 | Locate the TUTORIALS card | Action completes without error and produces the expected UI state. |
| 3 | Click the "More..." link at the bottom of the card | Control responds; expected next state is shown. |
| 4 | Verify the user is redirected to a page listing all available tutorials | Condition holds as described. |
| 5 | Verify the page loads without errors and displays more tutorials than shown in the card preview | Condition holds as described. |

---

## Expected Final State

Verify the page loads without errors and displays more tutorials than shown in the card preview.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Tutorials "More..." redirects to full tutorials list.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
