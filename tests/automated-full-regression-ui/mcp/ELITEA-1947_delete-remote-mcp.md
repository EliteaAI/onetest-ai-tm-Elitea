---
id: ELITEA-1947
title: "Delete Remote MCP"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_delete_remote.test_delete_remote_mcp
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/621
---

# ELITEA-1947: Delete Remote MCP

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP can be permanently deleted through the three-dot menu, and that the deletion is confirmed via dialog and persisted after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_mcp_to_delete |
| URL | https://mcp.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Remote MCP named "autotest_mcp_to_delete" with URL "https://mcp.example.com/sse" | MCP is created successfully |
| 2 | Verify it appears in MCP list | MCP appears in the list |
| 3 | Open MCP detail page | Detail page loads |
| 4 | Click three-dot menu button | Menu opens |
| 5 | Click "Delete" menu item | Delete action is triggered |
| 6 | Verify confirmation dialog appears | Confirmation dialog is displayed |
| 7 | Confirm deletion | Deletion is confirmed |
| 8 | Verify redirect to MCP list page | User is redirected to the MCP list |
| 9 | Verify "autotest_mcp_to_delete" no longer appears in list | MCP is absent from the list |
| 10 | Reload page — verify deletion persisted | MCP is still absent after reload |

---

## Expected Final State

The MCP "autotest_mcp_to_delete" is permanently removed from the MCP list and does not reappear after a page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP is deleted and absent from the list after reload.

**Fail:**
- Any step produces an error or unexpected result.
- MCP remains in the list after deletion or confirmation dialog is missing.
