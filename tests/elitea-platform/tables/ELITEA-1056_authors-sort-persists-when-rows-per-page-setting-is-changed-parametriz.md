---
id: ELITEA-1056
title: "Authors Sort Persists When Rows Per Page Setting Is Changed [Parametrized]"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1056: Authors Sort Persists When Rows Per Page Setting Is Changed [Parametrized]

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that changing the rows-per-page value while Authors sort is active does not reset or lose the sort — the table re-renders with the new page size while maintaining the sort order.

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
- Entity table has at least 15 items to allow meaningful rows-per-page changes.
- Table View is active with pagination controls visible.

**Steps (repeat for each selected row):**
1. Navigate to the entity table.
2. Click the Authors column header to sort ascending.
3. Confirm the sort indicator is visible. Note the first 3 items on page 1 (author names).
4. Locate the rows-per-page selector and change it to a different value (e.g., switch from 10 to 20, or from 20 to 10).
5. Observe the Authors column header and the row order after the page re-renders.
6. Change the rows-per-page value once more.
7. Observe the Authors column header and the row order.

**Expected Results:**
- Step 5: The Authors sort indicator remains visible (ascending); items are still sorted by author name after the re-render.
- Step 7: Sort is still active after a second rows-per-page change.
- The first items visible on the new page follow the correct alphabetical sequence — they are not in default/creation order.
- Total item count remains unchanged.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that changing the rows-per-page value while Authors sort is active does not reset or lose the sort — the table re-renders with the new page size while maintaining the sort order.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
