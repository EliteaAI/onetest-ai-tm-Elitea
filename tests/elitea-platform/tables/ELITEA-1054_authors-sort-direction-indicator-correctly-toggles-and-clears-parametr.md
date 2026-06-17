---
id: ELITEA-1054
title: "Authors Sort Direction Indicator Correctly Toggles and Clears [Parametrized]"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1054: Authors Sort Direction Indicator Correctly Toggles and Clears [Parametrized]

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the Authors column header cycles through ascending → descending → cleared states, and that the sort indicator disappears when another column is clicked.

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
- Entity table has at least 5 items with at least 2 distinct authors.
- Table View is active and no sort is currently applied (or sort is on a different column).

**Steps (repeat for each selected row):**
1. Navigate to the entity table.
2. Click the Authors column header once.
3. Observe the sort indicator on the Authors header and the row order.
4. Click the Authors column header a second time.
5. Observe the sort indicator and the row order.
6. Click any other sortable column header (e.g., Name or Created).
7. Observe the Authors column header.

**Expected Results:**
- Step 2: An ascending sort indicator (↑ arrow) appears on the Authors header; rows are ordered A→Z by author name.
- Step 4: The sort indicator changes to descending (↓ arrow); rows reorder Z→A by author name.
- Step 6: The Authors column header no longer shows any sort indicator; the newly clicked column shows its own sort indicator.
- Only one column shows an active sort indicator at a time.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that clicking the Authors column header cycles through ascending → descending → cleared states, and that the sort indicator disappears when another column is clicked.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
