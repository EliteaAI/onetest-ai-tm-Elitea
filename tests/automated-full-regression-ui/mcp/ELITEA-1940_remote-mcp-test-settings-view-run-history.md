---
id: ELITEA-1940
title: "Remote MCP — Test Settings — View Run History"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_test_settings_view_run_history.test_mcp_view_run_history_and_entry_details
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1736
---

# ELITEA-1940: Remote MCP — Test Settings — View Run History

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the run history panel in the Test Settings area lists previous tool executions with timestamps, and that selecting a history entry displays the input/output details.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP with at least one previous tool execution is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page | Detail page loads |
| 2 | Run a tool at least once to generate execution history | Tool run completes and generates a history entry |
| 3 | Click "view run history" button in test panel header | Run history panel/drawer opens |
| 4 | Verify run history panel/drawer opens | History panel is visible |
| 5 | Verify previous executions are listed with timestamps | Entries show execution timestamps |
| 6 | Click on a history entry — verify it shows input/output details | Input and output details are displayed for the selected entry |

---

## Expected Final State

The run history panel displays all previous executions with timestamps, and clicking an entry reveals its input/output details.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Run history entries are listed with timestamps and detail view works.

**Fail:**
- Any step produces an error or unexpected result.
- History entries are missing, timestamps are absent, or detail view does not open.
