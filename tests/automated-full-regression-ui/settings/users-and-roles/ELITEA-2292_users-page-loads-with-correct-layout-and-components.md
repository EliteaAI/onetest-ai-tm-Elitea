---
id: ELITEA-2292
title: "Users page loads with correct layout and components"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2292: Users page loads with correct layout and components

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Users page loads with correct layout and components. Success is confirmed when verify the page does not show any errors or permanent loading state.

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
| 1 | Log in as a user with Admin role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings → Users | Target page/section loads successfully. |
| 3 | Verify the page header shows "Users" | Condition holds as described. |
| 4 | Verify the following header-level components are present: | Condition holds as described. |
| 5 | Search input field | Action completes without error and produces the expected UI state. |
| 6 | Edit (pencil) icon button | Action completes without error and produces the expected UI state. |
| 7 | Delete (trash) icon button | Operation completes successfully; state updates and confirmation is shown. |
| 8 | "+" button to invite users | Action completes without error and produces the expected UI state. |
| 9 | Verify the users table has the following columns: | Condition holds as described. |
| 10 | Checkbox (for batch selection) | Action completes without error and produces the expected UI state. |
| 11 | Name (sortable ↕) | Action completes without error and produces the expected UI state. |
| 12 | Email (sortable ↕) | Action completes without error and produces the expected UI state. |
| 13 | Last login (sortable ↕) | Action completes without error and produces the expected UI state. |
| 14 | Role | Action completes without error and produces the expected UI state. |
| 15 | Actions (per-row Edit pencil + Delete trash icons) | Action completes without error and produces the expected UI state. |
| 16 | Verify each row shows: name, email, last login in ISO datetime format, role label, and action icons | Condition holds as described. |
| 17 | Verify the page does not show any errors or permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not show any errors or permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Users page loads with correct layout and components.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
