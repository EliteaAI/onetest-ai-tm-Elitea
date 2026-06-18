---
id: ELITEA-1060
title: "Authors Column Is Sortable in Table View [Parametrized — All Entity Types]"
priority: critical
type: functional
module: tables
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, issue:3677]
requirements: [ProjectAlita/projectalita.github.io#3677]
---
# ELITEA-1060: Authors Column Is Sortable in Table View [Parametrized — All Entity Types]

**Module:** Tables · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Authors column header in Table View is interactive (sortable) for all six entity types: Agents, Pipelines, Credentials, Toolkits, MCPs, and Apps.

**Parametrized rows (all 6 are mandatory):**

| # | Entity Type | Navigation Path |
|---|---|---|
| 1 | Agents | Left nav → Agents → Table View |
| 2 | Pipelines | Left nav → Pipelines → Table View |
| 3 | Credentials | Left nav → Credentials → Table View |
| 4 | Toolkits | Left nav → Toolkits → Table View |
| 5 | MCPs | Left nav → MCPs → Table View |
| 6 | Apps | Left nav → Apps → Table View |

**Pre-conditions:**
- User is logged in with access to a project containing at least 3 items of each entity type with different authors.
- Table View is active for each entity page.

**Steps (repeat for each parametrized row):**
1. Navigate to the entity table listed in the current row.
2. Confirm the table displays an Authors column.
3. Observe the Authors column header — note whether a sort icon (arrow/chevron) is visible or appears on hover.
4. Click the Authors column header.
5. Observe the table rows and the column header indicator.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | (See description above) |  |

## Expected Final State

- Step 3: A sort affordance (hover icon or static sort arrow) is visible on the Authors column header.
- Step 4: The table rows reorder — items sorted by author name (ascending by default).
- Step 5: A directional sort indicator (ascending arrow) is displayed on the Authors column header.
- No JavaScript console errors are thrown.
- Behavior is identical across all 6 entity types.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
