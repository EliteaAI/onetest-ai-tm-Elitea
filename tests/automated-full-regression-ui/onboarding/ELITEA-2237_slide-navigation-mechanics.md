---
id: ELITEA-2237
title: "Onboarding — Slide Navigation Mechanics"
priority: high
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2237: Onboarding — Slide Navigation Mechanics

**Module:** onboarding · **Priority:** high · **Type:** functional

**Objective:** Verify the onboarding slide navigation controls work correctly, including forward/backward navigation and boundary conditions (first/last slide arrow states).

---

## Preconditions

- User is logged in to the Elitea platform.
- Onboarding tips card is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to the application for the first time and verify the onboarding card is at slide 1/48 | User is authenticated and lands on the onboarding card at slide 1/48. |
| 2 | Verify the left arrow (<) / Back button is visually inactive (disabled/greyed out) on slide 1/48 | Condition holds as described. |
| 3 | Click the left arrow (<) and verify no navigation occurs (stays on slide 1/48) | Control is disabled; no navigation occurs. |
| 4 | Verify the right arrow (>) / Next button is active and clickable | Condition holds as described. |
| 5 | Click the right arrow (>) | Control responds; slide advances. |
| 6 | Verify the slide counter advances to "2 / 48" | Condition holds as described. |
| 7 | Verify the slide content updates to "Tip 2: Navigate the Sidebar" | Condition holds as described. |
| 8 | Verify the description for slide 2 is displayed correctly | Condition holds as described. |
| 9 | Click the right arrow (>) again | Control responds; slide advances. |
| 10 | Verify the counter advances to "3 / 48" and new tip content is shown | Condition holds as described. |
| 11 | Click the right arrow (>) repeatedly until slide 48/48 is reached | Control responds; slides advance through all content. |
| 12 | Verify the slide counter shows "48 / 48" | Condition holds as described. |
| 13 | Verify the slide content shows "Tip 48: View Message Execution Details" | Condition holds as described. |
| 14 | Verify the right arrow (>) / Next button is visually inactive (disabled/greyed out) on slide 48/48 | Condition holds as described. |
| 15 | Click the right arrow (>) and verify no navigation occurs (stays on slide 48/48) | Control is disabled; no navigation occurs. |
| 16 | Verify the left arrow (<) / Back button is now active and clickable on slide 48/48 | Condition holds as described. |
| 17 | Click the left arrow (<) | Control responds; slide moves backward. |
| 18 | Verify the counter moves to "47 / 48" and previous slide content is shown | Condition holds as described. |

---

## Expected Final State

The slide navigation controls work correctly: forward navigation advances through all 48 slides with content updating properly, backward navigation moves to previous slides, and boundary conditions are enforced (left arrow inactive on slide 1, right arrow inactive on slide 48).

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified: Left arrow inactive on slide 1, right arrow navigates forward correctly, slide content and counter update properly, right arrow inactive on slide 48, left arrow navigates backward correctly.

**Fail:**
- Any assertion fails, navigation does not work as expected, or boundary conditions are not enforced.

---

## Notes

**Source functional tests:** ELITEA-2237, ELITEA-2238

**Regression rationale:** Consolidated from 2 tests to verify all slide navigation mechanics in a single flow. This ensures both forward/backward navigation and boundary conditions (inactive arrows at slide 1 and 48) are validated together.

**Selected checkpoints:** Left arrow disabled on slide 1, forward navigation through multiple slides, slide counter progression (1/48 → 2/48 → 3/48 → ... → 48/48), slide content updates, right arrow disabled on slide 48, backward navigation functionality.
