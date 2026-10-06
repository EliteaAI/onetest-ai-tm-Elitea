---
id: ELITEA-2226
title: "Help Center — Sidebar Interactive Tour starts when clicking the link"
priority: medium
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2226: Help Center — Sidebar Interactive Tour starts when clicking the link

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Sidebar Interactive Tour starts when clicking the link. Success is confirmed when verify three navigation buttons are visible: skip, back(inactive/grey colored), next.

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
| 2 | Locate the INTERACTIVE TOURS card (red/maroon icon, subtitle: "Guided tours to explore key features and workflows") | Action completes without error and produces the expected UI state. |
| 3 | Verify the links "Sidebar Interactive Tour" and "Chat Interactive Tour" are displayed | Condition holds as described. |
| 4 | Click the "Sidebar Interactive Tour" link | Control responds; expected next state is shown. |
| 5 | Verify the interactive tour overlay launches immediately | Condition holds as described. |
| 6 | Verify the first tour step is displayed as a tooltip/popover anchored to the ELITEA Logo in the sidebar | Condition holds as described. |
| 7 | Verify the first step description reads: "The ELITEA Logo in the sidebar shows the server status. Green mark points that server is working. Red mark points that server is updating." | Condition holds as described. |
| 8 | Verify the step counter shows current step out of total steps (e.g., "1 / 17") | Condition holds as described. |
| 9 | Verify three navigation buttons are visible: Skip, Back(inactive/grey colored), Next | Condition holds as described. |

---

## Expected Final State

Verify three navigation buttons are visible: Skip, Back(inactive/grey colored), Next.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Sidebar Interactive Tour starts when clicking the link.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
