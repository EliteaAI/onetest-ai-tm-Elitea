---
id: ELITEA-3753
title: "Help Center — page loads successfully via sidebar icon"
priority: medium
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-3753: Help Center — page loads successfully via sidebar icon

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — page loads successfully via sidebar icon. Success is confirmed when verify the application version "version: x.x.x (dd-mon-yyyy)" is displayed in the top right corner with "i" in circle icon near it.

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
| 1 | Locate the "?" (Help Center) icon at the bottom of the left sidebar next to "Support Bot" | Action completes without error and produces the expected UI state. |
| 2 | Click the "?" icon | Control responds; expected next state is shown. |
| 3 | Verify the Help Center page opens | Condition holds as described. |
| 4 | Verify the page title "Help Center" is displayed in the top left header | Condition holds as described. |
| 5 | Verify the page subtitle "Explore Help Center" and description "Guides, documentation, and release notes to support your work." are displayed | Condition holds as described. |
| 6 | Verify four resource cards are visible: DOCUMENTATION, RELEASE NOTES, VIDEO LIBRARY, TUTORIALS, INTERACTIVE TOURS | Condition holds as described. |
| 7 | Verify all the cards (e.g.INTERACTIVE TOURS) are visible with their links: (e.g. "Sidebar Interactive Tour" and "Chat Interactive Tour") | Condition holds as described. |
| 8 | Verify each card shows its icon, title, and subtitle description | Condition holds as described. |
| 9 | Verify the application version "Version: X.X.X (DD-Mon-YYYY)" is displayed in the top right corner with "i" in circle icon near it | Condition holds as described. |

---

## Expected Final State

Verify the application version "Version: X.X.X (DD-Mon-YYYY)" is displayed in the top right corner with "i" in circle icon near it.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — page loads successfully via sidebar icon.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
