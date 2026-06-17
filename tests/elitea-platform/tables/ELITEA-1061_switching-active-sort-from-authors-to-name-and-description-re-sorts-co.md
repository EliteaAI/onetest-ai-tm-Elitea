---
id: ELITEA-1061
title: "Switching Active Sort from Authors to Name and Description Re-sorts Correctly [Parametrized]"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1061: Switching Active Sort from Authors to Name and Description Re-sorts Correctly [Parametrized]

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that after sorting by Authors, clicking a different sortable column (Name or Description) correctly re-sorts the table by the new column and clears the Authors sort indicator.

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
- Entity table has at least 5 items with varied names and authors.
- Table View is active.

**Steps (repeat for each selected row):**
1. Navigate to the entity table.
2. Click the Authors column header to apply Authors sort (ascending).
3. Note the current row order (sorted by author name).
4. Click the Name column header.
5. Observe the row order and column sort indicators.
6. Click the Name column header again (descending).
7. Observe the row order — items should now be sorted Z→A by name.
8. Click the Authors column header once more.
9. Observe the row order and column sort indicators.

**Expected Results:**
- Step 4: Rows re-sort by Name (A→Z); Authors column header sort indicator disappears; Name column shows ascending indicator.
- Step 6: Rows re-sort by Name Z→A; Name column shows descending indicator.
- Step 8: Rows re-sort by Author (A→Z); Name column indicator disappears; Authors column shows ascending indicator.
- At no point do two columns simultaneously show an active sort indicator.
- No items are lost or duplicated during sort column switching.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that after sorting by Authors, clicking a different sortable column (Name or Description) correctly re-sorts the table by the new column and clears the Authors sort indicator.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
