---
id: ELITEA-2226
title: "Help Center — Interactive Tour Navigation Controls"
priority: high
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2226: Help Center — Interactive Tour Navigation Controls

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that the Sidebar Interactive Tour launches correctly, all navigation controls (Next, Back, Skip) function as expected, and the tour exits gracefully when Skip is clicked, returning the application to a fully functional state.

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
| **TOUR START** | | |
| 1 | Navigate to Help Center | Help Center page loads successfully |
| 2 | Locate the INTERACTIVE TOURS card (red/maroon icon, subtitle: "Guided tours to explore key features and workflows") | Card is visible |
| 3 | Verify the links "Sidebar Interactive Tour" and "Chat Interactive Tour" are displayed | Both tour links are visible |
| 4 | Click the "Sidebar Interactive Tour" link | Link is clickable |
| 5 | Verify the interactive tour overlay launches immediately | Tour overlay appears |
| 6 | Verify the first tour step is displayed as a tooltip/popover anchored to the ELITEA Logo in the sidebar | Tooltip is anchored to sidebar logo |
| 7 | Verify the first step description reads: "The ELITEA Logo in the sidebar shows the server status. Green mark points that server is working. Red mark points that server is updating." | Step 1 description is correct |
| 8 | Verify the step counter shows "1 / 17" | Step counter displays 1 out of 17 |
| 9 | Verify three navigation buttons are visible: Skip, Back (inactive/grey colored), Next | All three buttons visible; Back is disabled |
| **NEXT NAVIGATION** | | |
| 10 | Click "Next" to advance to step 2 | Tour advances to step 2/17 |
| 11 | Verify the step counter updates to "2 / 17" | Step counter shows 2 of 17 |
| 12 | Verify the Back button is now active/enabled | Back button is clickable |
| **BACK NAVIGATION** | | |
| 13 | Click the "Back" button | Tour returns to previous step |
| 14 | Verify the tour returns to step 1/17 | Step counter shows 1 of 17 |
| 15 | Verify the tooltip content matches the content of step 1 | Step 1 description is displayed |
| 16 | Verify the Back button is disabled/inactive on step 1 | Back button is greyed out |
| **SKIP FUNCTIONALITY** | | |
| 17 | Click "Next" to advance to step 3 | Tour advances to step 3/17 |
| 18 | Verify step counter shows "3 / 17" | Step counter is updated |
| 19 | Click the "Skip" button | Skip button is clickable |
| 20 | Verify the tour overlay and tooltip close immediately | Tour UI is dismissed |
| 21 | Verify the user is returned to the project's default view (e.g., Chats page or last visited page) | Application returns to normal view |
| 22 | Verify no tour overlay or highlighted elements remain on screen | No tour artifacts visible |
| 23 | Verify the application is fully functional after skipping (navigation and sidebar items are all accessible) | All UI elements are accessible and functional |

---

## Expected Final State

The Sidebar Interactive Tour launches successfully, all navigation controls (Next, Back, Skip) work correctly, the Back button is disabled on step 1, and clicking Skip gracefully terminates the tour and returns the application to a fully functional state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Tour starts at step 1/17 with correct button states; Next advances steps; Back returns to previous step and is disabled on step 1; Skip closes the tour and returns the app to a functional state.

**Fail:**
- Any step produces an error or unexpected result.
- Navigation controls do not function correctly, or the application is not fully functional after skipping the tour.

---

## Notes

**Source functional tests:** ELITEA-2226 (Tour starts), ELITEA-2230 (Back button navigation), ELITEA-2229 (Skip terminates tour)

**Regression rationale:** Consolidates the Interactive Tour navigation controls into one comprehensive journey. All three tests validate the same tour's control mechanisms: tour launch, step navigation (Next/Back), and graceful exit (Skip). Testing these controls together ensures the tour navigation pattern works cohesively from start to skip, while validating Back button state management (disabled on first step) and post-skip application functionality.

**Selected checkpoints:** Tour overlay launches; step 1/17 displayed with correct description and button states (Back disabled); Next advances to step 2; Back returns to step 1 and disables; Next to step 3; Skip closes tour immediately; application returns to normal view; no tour artifacts remain; all UI elements functional after skip.
