---
id: ELITEA-1921
title: "Create Remote MCP — Minimal Required Fields"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_create_remote.test_create_remote_mcp_minimal_required_fields
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/634
---

# ELITEA-1921: Create Remote MCP — Minimal Required Fields

**Module:** elitea-platform · **Priority:** high · **Type:** functional

**Objective:** Verify that a Remote MCP can be created successfully by providing only the mandatory fields (Toolkit Name and URL), and that the new entry appears correctly in the MCP list with a "Remote" type badge.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has access to the MCPs section in the left navigation.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_remote_mcp_minimal |
| URL | https://mcp.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCPs section from sidebar (click "MCPs" button in left nav) | MCPs section loads in the sidebar |
| 2 | Click the "+" button next to "MCP" label in the sidebar header area | MCP creation flow initiates |
| 3 | Verify "Choose the MCP type" page appears at URL /app/mcps/create | Page displays at the correct URL |
| 4 | Verify two sections displayed: "Local" (with message "Still no local MCP available...") and "Remote" (with "Remote MCP" card) | Both sections are visible with correct content |
| 5 | Click the "Remote MCP" card | Form page navigates to /app/mcps/create/mcp with "New Remote MCP" tab selected |
| 6 | Verify form appears at URL /app/mcps/create/mcp with tab "New Remote MCP" selected | Correct URL and tab are active |
| 7 | Verify Save button is disabled when form is empty | Save button is disabled |
| 8 | Fill "Toolkit Name *" field with "autotest_remote_mcp_minimal" | Field accepts input and displays "autotest_remote_mcp_minimal" |
| 9 | Fill "Url *" field with "https://mcp.example.com/sse" | Field accepts input and displays the URL |
| 10 | Verify Save button becomes enabled | Save button is now clickable |
| 11 | Click Save | Operation completes successfully; redirect occurs |
| 12 | Verify redirect to MCP detail page with name "autotest_remote_mcp_minimal" | Detail page loads with the correct MCP name |
| 13 | Navigate to MCP list — verify new MCP appears with "Remote" type badge | New MCP is listed with "Remote" badge |

---

## Expected Final State

The MCP "autotest_remote_mcp_minimal" is visible in the MCP list with a "Remote" type badge and its detail page is accessible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The MCP is created and displayed in the list with the correct "Remote" type badge.

**Fail:**
- Any step produces an error or unexpected result.
- The MCP is not created or does not appear in the list.
