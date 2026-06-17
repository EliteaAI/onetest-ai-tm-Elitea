---
id: ELITEA-1057
title: "Authors Column Is Not Sortable When All Items Belong to a Single Author [Parametrized]"
priority: medium
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1057: Authors Column Is Not Sortable When All Items Belong to a Single Author [Parametrized]

**Module:** Tables · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the behavior of the Authors column header when all items in the table belong to a single author — the column should either be visually non-interactive (no sort affordance) or, if clickable, produce no meaningful reordering while remaining stable.

**Parametrized rows (pick any 1 of the 6 entity types):**

| # | Entity Type |
|---|---|
| 1 | Agents |
| 2 | Pipelines |
| 3 | Credentials |
| 4 | Toolkits |
| 5 | MCPs |
| 6 | Apps |

**Pre-conditions:**
- All items in the selected entity table are created/owned by exactly one user (the currently logged-in user, or filtered to a project with a single contributor).
- At least 3 items exist.
- Table View is active.

**Steps:**
1. Navigate to the entity table.
2. Observe the Authors column — note whether a sort icon is shown or appears on hover.
3. Click the Authors column header.
4. Observe whether the rows reorder, whether a sort indicator appears, and whether any error occurs.
5. Click the Authors column header a second time.
6. Observe behavior.

**Expected Results:**
- Step 2: The Authors column header ideally does not show a sort affordance (no hover icon), OR the affordance is visually muted/disabled. (Exact behavior depends on implementation.)
- Step 3: Either (a) nothing happens — no sort applied, no indicator shown; OR (b) a sort is applied but the row order is unchanged (since all authors are the same).
- Step 4: No JavaScript errors, no page crash, no broken UI state.
- Step 5-6: Consistent behavior — no unexpected toggle into a broken state.
- The table never becomes unresponsive or displays a loading error from sorting a single-author dataset.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify the behavior of the Authors column header when all items in the table belong to a single author — the column should either be visually non-interactive (no sort affordance) or, if clickable, produce no meaningful reordering while remaining stable.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
