---
id: ELITEA-2229
title: "Help Center — clicking Skip during Sidebar Interactive Tour terminates the tour"
priority: high
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2229: Help Center — clicking Skip during Sidebar Interactive Tour terminates the tour

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that Help Center — clicking Skip during Sidebar Interactive Tour terminates the tour. Success is confirmed when verify the application is fully functional after skipping (navigation and sidebar items are all accessible).

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
| 1 | Navigate to Help Center and click "Sidebar Interactive Tour" | Target page/section loads successfully. |
| 2 | Verify the tour starts at step 1/17 with Skip, Back, and Next buttons visible | Condition holds as described. |
| 3 | Click the "Next" button to advance to step 3/17 | Control responds; expected next state is shown. |
| 4 | Click the "Skip" button | Control responds; expected next state is shown. |
| 5 | Verify the tour overlay and tooltip close immediately | Condition holds as described. |
| 6 | Verify the user is returned to the project's default view (e.g., Chats page or last visited page) | Condition holds as described. |
| 7 | Verify no tour overlay or highlighted elements remain on screen | Condition holds as described. |
| 8 | Verify the application is fully functional after skipping (navigation and sidebar items are all accessible) | Condition holds as described. |

---

## Expected Final State

Verify the application is fully functional after skipping (navigation and sidebar items are all accessible).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — clicking Skip during Sidebar Interactive Tour terminates the tour.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
