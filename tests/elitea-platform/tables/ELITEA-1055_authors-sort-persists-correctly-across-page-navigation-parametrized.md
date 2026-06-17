---
id: ELITEA-1055
title: "Authors Sort Persists Correctly Across Page Navigation [Parametrized]"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1055: Authors Sort Persists Correctly Across Page Navigation [Parametrized]

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that when Authors sort is active and the user navigates to a different page (page 2, page 3, or back to page 1), the sort remains active — the sort indicator is still shown and items on the new page are correctly sorted.

**Parametrized rows (pick any 2 of the 6 entity types):**

| # | Entity Type |
|---|---|
| 1 | Agents |
| 2 | Pipelines |
| 3 | Credentials |
| 4 | Toolkits |
| 5 | MCPs |
| 6 | Apps |

**Pre-conditions:**
- Entity table has enough items to span at least 2 pages (pagination controls are visible).
- Table View is active.

**Steps (repeat for each selected row):**
1. Navigate to the entity table.
2. Click the Authors column header to sort ascending.
3. Confirm the sort indicator is visible and page 1 shows correctly sorted items.
4. Click the "Next page" control to navigate to page 2.
5. Observe the Authors column header and the row order on page 2.
6. Navigate back to page 1 using the "Previous page" control.
7. Observe the Authors column header and the row order on page 1.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | (See description above) |  |

## Expected Final State

- Step 4: After navigating to page 2, the Authors sort indicator remains visible (ascending).
- Step 5: Items on page 2 are a continuation of the ascending alphabetical author sort — no unsorted or randomly ordered rows.
- Step 6: Returning to page 1 still shows the Authors ascending indicator and correct sorted items.
- The sort is never silently reset by a page navigation event.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
