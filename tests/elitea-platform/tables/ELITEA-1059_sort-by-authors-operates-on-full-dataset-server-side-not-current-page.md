---
id: ELITEA-1059
title: "Sort by Authors Operates on Full Dataset (Server-side), Not Current Page Only [Parametrized]"
priority: critical
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1059: Sort by Authors Operates on Full Dataset (Server-side), Not Current Page Only [Parametrized]

**Module:** Tables · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that sorting by Authors triggers a server-side sort of the complete dataset, not a client-side re-sort of only the currently visible page.

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
- The selected entity table contains more items than fit on one page (pagination is active, at least 2 pages).
- Items span at least 3 distinct authors with names spanning a wide alphabetical range (e.g., authors starting with A, M, Z).
- Table View is active.

**Steps (repeat for each selected row):**
1. Navigate to the entity table.
2. Note the authors visible on page 1 (unsorted / default order). Record the last author visible on page 1.
3. Click the Authors column header to sort ascending.
4. Observe all authors on page 1 — they should be at the beginning of the alphabetical range.
5. Navigate to page 2.
6. Observe the authors on page 2 — they should continue alphabetically from where page 1 left off.
7. Navigate back to page 1 and click Authors header again (descending sort).
8. Navigate to page 2 again.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | (See description above) |  |

## Expected Final State

- Step 3: Page 1 shows items with the earliest-alphabetical authors.
- Step 6: Page 2 authors continue the sort sequence (later in alphabet) — they are NOT a re-ordering of the page-1 items.
- Step 8: Page 2 shows items with relatively earlier-alphabet authors compared to page 1 (descending sequence continues).
- No items are duplicated or missing across pages.
- Total item count remains unchanged across sort operations.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
