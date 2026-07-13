---
id: ELITEA-1961
title: "MCP — Back Navigation from Detail to List"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1961: MCP — Back Navigation from Detail to List

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the back button on an MCP detail page returns the user to the MCP list page while preserving the list state such as scroll position and applied filters.

---

## Preconditions

- User is logged in to the Elitea platform.
- MCP list page has at least one MCP available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP list page | MCP list page loads |
| 2 | Click on any MCP card to open detail page | MCP detail page loads |
| 3 | Verify detail page loads with back button (arrow icon, top-left of main content) | Back button is visible |
| 4 | Click back button | Navigation is triggered |
| 5 | Verify navigation returns to MCP list page | MCP list page is displayed |
| 6 | Verify list state is preserved (same scroll position, filters still applied if any) | List state matches the state before opening the detail page |

---

## Expected Final State

The user is back on the MCP list page with the same scroll position and filters as before opening the detail page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Back button navigates to MCP list page; list state is preserved.

**Fail:**
- Any step produces an error or unexpected result.
- Back button is missing, navigation fails, or list state is not preserved.
