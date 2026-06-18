---
id: ELITEA-1058
title: "Authors Sort Correctly Handles Pinned Items [Parametrized]"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1058: Authors Sort Correctly Handles Pinned Items [Parametrized]

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the Authors sort is applied, pinned items are handled correctly — either remaining at the top of the list (above sorted items) or being included in the sort pool alongside unpinned items — and that the behavior is consistent and predictable.

**Parametrized rows (pick any 1 of the 6 entity types that supports pinning):**

| # | Entity Type |
|---|---|
| 1 | Agents |
| 2 | Pipelines |
| 3 | Credentials |
| 4 | Toolkits |
| 5 | MCPs |
| 6 | Apps |

**Pre-conditions:**
- The selected entity table contains at least 5 items.
- At least 1 item is pinned (bookmarked / starred).
- Pinned item's author name is NOT the alphabetically first or last — it is somewhere in the middle (to make sort interaction observable).
- Table View is active.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the entity table. |  |
| 2 | Confirm that the pinned item is visible at/near the top in the default unsorted view. |  |
| 3 | Click the Authors column header to sort ascending. |  |
| 4 | Observe the position of the pinned item and the positions of all other items. |  |
| 5 | Click the Authors column header again to sort descending. |  |
| 6 | Observe the position of the pinned item again. |  |
| 7 | Click the Authors column header or another column to clear the sort. |  |
| 8 | Observe whether the pinned item returns to its pinned position. |  |

## Expected Final State

- Step 4 (ascending sort): Either (a) pinned item remains at the very top regardless of sort, OR (b) pinned item moves to its alphabetical position in the sorted list. The behavior must be one of these two — no duplicate rendering, no disappearance, no UI error.
- Step 6 (descending sort): Consistent with step 4 behavior — pinned item is either still at top or at its correct descending position.
- Step 8: After clearing sort, pinned item returns to its pinned position at the top (if option a was in effect) or to its default order position (if option b).
- No layout glitches or broken rows occur during sort operations on a table with pinned items.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
