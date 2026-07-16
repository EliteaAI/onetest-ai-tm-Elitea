---
id: ELITEA-1941
title: "MCP Dashboard — Search by Name"
priority: high
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_search_by_name.TestMcpSearchByName.test_mcp_search_by_name
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/586
---

# ELITEA-1941: MCP Dashboard — Search by Name

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the search box on the MCP list page correctly filters MCPs by name, showing only matching results and restoring all MCPs when the search is cleared.

---

## Preconditions

- User is logged in to the Elitea platform.
- Multiple MCPs exist in the project including at least one named "Web Search".

---

## Test Data

| Field | Value |
|-------|-------|
| Search term (match) | Web |
| Search term (no match) | nonexistent_xyz_mcp |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP list page (/app/mcps/all) | MCP list page loads |
| 2 | Verify search textbox is visible with placeholder "Let's find something amazing!" | Search box is displayed with correct placeholder |
| 3 | Type "Web" in search box | Filter is applied |
| 4 | Verify only MCPs with "Web" in name are shown (e.g., "Web Search") | Only matching MCPs are visible |
| 5 | Clear search and type "nonexistent_xyz_mcp" | Filter is updated |
| 6 | Verify no results shown (empty state or "no results" message) | Empty state or no-results message is displayed |
| 7 | Clear search — verify all MCPs reappear | All MCPs are visible again |

---

## Expected Final State

The MCP list returns to showing all MCPs after the search is cleared.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Search correctly filters results and clears to show all MCPs.

**Fail:**
- Any step produces an error or unexpected result.
- Search does not filter correctly or MCPs do not reappear after clearing.
