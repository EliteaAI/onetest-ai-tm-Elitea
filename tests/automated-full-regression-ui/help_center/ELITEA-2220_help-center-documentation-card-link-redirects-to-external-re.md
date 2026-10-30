---
id: ELITEA-2220
title: "Help Center — Card Links Navigation"
priority: medium
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2220: Help Center — Card Links Navigation

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center resource cards (Documentation, Release Notes, Tutorials) correctly redirect to their respective external pages when links are clicked, and that target pages load without errors.

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
| **DOCUMENTATION Card** | | |
| 1 | Navigate to Help Center | Help Center page loads successfully |
| 2 | Locate the DOCUMENTATION card (blue icon, subtitle: "API reference, guides, and platform concepts") | Card is visible with correct icon and subtitle |
| 3 | Verify links displayed: Getting Started, How-To Guides, Integrations, Migration & Update | All four links are visible |
| 4 | Click the "Getting Started" link | Link is clickable |
| 5 | Verify the user is redirected to the relevant documentation page in a new tab or window | Redirect occurs to external documentation |
| 6 | Verify the target page loads without errors | Documentation page loads successfully |
| **RELEASE NOTES Card** | | |
| 7 | Return to Help Center page | Help Center page is displayed |
| 8 | Locate the RELEASE NOTES card (orange icon, subtitle: "Product updates, improvements, and fixes") | Card is visible with correct icon and subtitle |
| 9 | Verify links displayed according to current/recent release versions (e.g., Release 2.0.2 (latest), Release 2.0.1, Release 2.0.0, Release 2.0.0B2) | Release version links are visible |
| 10 | Click the latest release link (e.g., "Release 2.0.2 (latest)") | Link is clickable |
| 11 | Verify the user is redirected to the release notes page for the selected version | Redirect occurs to release notes page |
| 12 | Verify the target page loads without errors | Release notes page loads successfully |
| **TUTORIALS Card** | | |
| 13 | Return to Help Center page | Help Center page is displayed |
| 14 | Locate the TUTORIALS card (green icon, subtitle: "Step-by-step guides and use cases") | Card is visible with correct icon and subtitle |
| 15 | Verify links displayed (e.g., Course: AI-Based EliteA Platform, How to create an Agent, How to create a Pipeline, More...) | Tutorial links are visible |
| 16 | Click the "How to create an Agent" link | Link is clickable |
| 17 | Verify the user is redirected to the correct tutorial page | Redirect occurs to tutorial resource |
| 18 | Verify the target page loads without errors | Tutorial page loads successfully |

---

## Expected Final State

All three resource cards (Documentation, Release Notes, Tutorials) successfully redirect to their respective external pages, and all target pages load without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each card link redirects to the correct external resource and the target page loads successfully.

**Fail:**
- Any step produces an error or unexpected result.
- Any card link fails to redirect or the target page fails to load.

---

## Notes

**Source functional tests:** ELITEA-2220 (Documentation card), ELITEA-2221 (Release Notes card), ELITEA-2222 (Tutorials card)

**Regression rationale:** Consolidates the card link navigation pattern into one comprehensive test. All three cards follow the same behavior: click link → verify redirect → verify page loads. Testing all three cards in sequence ensures the navigation pattern works consistently across different resource types while reducing redundant setup/teardown overhead.

**Selected checkpoints:** Card visibility and correct icon/subtitle; link presence; redirect to external resource; target page loads without errors for each card type.
