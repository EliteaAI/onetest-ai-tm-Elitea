---
id: ELITEA-1973
title: "Credential Dashboard — View Toggle (Table/Card)"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1973: Credential Dashboard — View Toggle (Table/Card)

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the credentials list supports switching between Card and Table views, that the Table view displays correct columns and pagination controls, and that the Card view is restored when switching back.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with multiple credentials (more than 20 to validate pagination).
- The Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Default page size (table view) | 20 items per page |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Credentials list | Credentials list page loads |
| 2 | Verify the default view is Card (card view button appears pressed/active) | Card view is the default and active |
| 3 | Click the Table view button | Credentials switch to table format |
| 4 | Verify credentials display in table format | Table layout is shown |
| 5 | Verify the table columns: Name & Description, Type, Authors, Created, Actions | All five columns are present |
| 6 | Verify pagination controls are present, defaulting to 20 items per page | Pagination controls are visible; 20 credentials shown |
| 7 | Click the next page control | Next set of credentials is displayed |
| 8 | Click the previous page control | Previous set of credentials is displayed |
| 9 | Click the Card view button | Credentials switch back to card format |
| 10 | Verify credentials display in card format | Card layout is restored |

---

## Expected Final State

The view toggle works in both directions; Table view shows the correct columns and pagination; Card view is restored on switching back.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Table view shows the correct 5 columns and 20-item pagination; Card view is restored correctly.

**Fail:**
- Any step produces an error or unexpected result.
- View toggle does not switch layouts, columns are missing, or pagination does not function.
