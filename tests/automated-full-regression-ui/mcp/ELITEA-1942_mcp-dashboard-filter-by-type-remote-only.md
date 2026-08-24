---
id: ELITEA-1942
title: "MCP Dashboard — Filter by Type (Remote only)"
priority: high
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_type_filter.test_mcp_dashboard_filter_by_type_remote
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1744
---

# ELITEA-1942: MCP Dashboard — Filter by Type (Remote only)

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Remote" type filter on the MCP list page shows only Remote MCPs and hides Local MCPs, and that removing the filter restores all MCPs.

---

## Preconditions

- User is logged in to the Elitea platform.
- Both Local MCPs (e.g., ADO, FileSystem, PlaywrightMCP) and Remote MCPs (e.g., Web Search) exist in the project.

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
| 2 | Verify "Types" label and filter buttons "Local" and "Remote" are visible in sidebar filter area | Both filter buttons are displayed |
| 3 | Click "Remote" filter button | Remote filter is applied |
| 4 | Verify only MCPs with "Remote" type badge are displayed | Only Remote MCPs are shown |
| 5 | Verify Local MCPs (e.g., "ADO", "FileSystem", "PlaywrightMCP") are hidden | Local MCPs are not visible |
| 6 | Click "Remote" again to deselect (or click elsewhere to clear) | Filter is deactivated |
| 7 | Verify all MCPs reappear | All MCPs are visible |

---

## Expected Final State

All MCPs (both Local and Remote) are displayed after the Remote filter is removed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Remote filter correctly hides Local MCPs and restores all on deselect.

**Fail:**
- Any step produces an error or unexpected result.
- Filter does not hide Local MCPs or all MCPs do not return after deselection.
