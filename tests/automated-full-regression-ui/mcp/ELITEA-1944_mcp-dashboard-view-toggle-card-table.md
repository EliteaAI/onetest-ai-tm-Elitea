---
id: ELITEA-1944
title: "MCP Dashboard — View Toggle (Card/Table)"
priority: high
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_view_toggle.test_mcp_dashboard_view_toggle_card_table
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/523
---

# ELITEA-1944: MCP Dashboard — View Toggle (Card/Table)

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the MCP list page supports switching between Card and Table view layouts, with Card view as the default, and that both layouts are accessible via the view toggle.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one MCP exists in the project.

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
| 2 | Verify "Small View Toggler" group is visible with Table view and Card list view buttons | View toggle group is displayed |
| 3 | Verify Card list view button is pressed (active) by default | Card view is the default active layout |
| 4 | Click Table view button | Table view is activated |
| 5 | Verify MCPs display in table/list format (layout changes from cards to rows) | MCPs are shown as table rows |
| 6 | Click Card list view button | Card view is re-activated |
| 7 | Verify MCPs display back in card format | MCPs are shown as cards |

---

## Expected Final State

MCPs are displayed in Card view after toggling back from Table view.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Layout changes correctly between Card and Table views.

**Fail:**
- Any step produces an error or unexpected result.
- Layout does not change, or toggle buttons do not respond.
