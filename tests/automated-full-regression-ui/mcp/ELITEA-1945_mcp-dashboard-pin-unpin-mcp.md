---
id: ELITEA-1945
title: "MCP Dashboard — Pin/Unpin MCP"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_pin_unpin.test_mcp_dashboard_pin_unpin
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1744
---

# ELITEA-1945: MCP Dashboard — Pin/Unpin MCP

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that an MCP card can be pinned to the top of the MCP list and unpinned back to its original position.

---

## Preconditions

- User is logged in to the Elitea platform.
- MCP list page is in Card view.
- At least one MCP card with a "Pin to top" button is visible.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP list page in Card view | MCP list loads in Card view |
| 2 | Identify an MCP card and locate "Pin to top" button | "Pin to top" button is visible on the card |
| 3 | Click "Pin to top" button on a specific MCP | MCP moves to top position in the list |
| 4 | Verify MCP moves to top position in the list | Selected MCP appears first in the list |
| 5 | Verify button tooltip/label changes to "Unpin from top" | Button label shows "Unpin from top" |
| 6 | Click "Unpin from top" button | MCP is unpinned |
| 7 | Verify MCP returns to its original position | MCP is no longer at the top |

---

## Expected Final State

The MCP is unpinned and no longer appears at the top of the list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pin moves MCP to top; unpin returns it to original position.

**Fail:**
- Any step produces an error or unexpected result.
- Pin/unpin actions have no effect or button label does not update.
