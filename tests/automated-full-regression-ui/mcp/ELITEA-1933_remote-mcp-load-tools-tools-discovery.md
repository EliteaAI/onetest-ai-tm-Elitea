---
id: ELITEA-1933
title: "Remote MCP — Load Tools (Tools Discovery)"
priority: high
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1933: Remote MCP — Load Tools (Tools Discovery)

**Module:** elitea-platform · **Priority:** high · **Type:** functional

**Objective:** Verify that a Remote MCP can discover and load available tools from a valid remote server, and that discovered tools are populated in both the Form view and the Raw JSON "available_mcp_tools" array.

---

## Preconditions

- User is logged in to the Elitea platform.
- A valid remote MCP server URL (e.g., Tavily SSE endpoint) is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_tools_discovery |
| URL | (valid remote MCP server SSE endpoint) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new Remote MCP with name "autotest_tools_discovery" | MCP creation form loads |
| 2 | Fill URL with a valid remote MCP server URL (e.g., Tavily or any SSE endpoint) | Field accepts and displays the URL |
| 3 | Save the MCP | MCP detail page loads |
| 4 | Verify Tools section shows "No tools to display for now. To get tools from MCP press button 'Load Tools'" | Correct empty-state message is shown |
| 5 | Click "Load Tools" button | Loading initiates (may show loading indicator) |
| 6 | Wait for tools to load | Tools load from the remote server |
| 7 | Verify discovered tools appear as buttons in the Tools section (each tool shows tool name) | Tool buttons are visible with tool names |
| 8 | Verify each discovered tool is clickable (shows tool details or schema on click) | Clicking a tool shows its details or schema |
| 9 | Switch to Raw Json — verify "available_mcp_tools" array populated with tool objects containing "label", "value", "args_schema" | JSON array contains expected tool objects |
| 10 | Verify "selected_tools" array contains names of discovered tools | selected_tools array is populated |

---

## Expected Final State

All discovered tools are visible in the Form view and reflected in the Raw JSON; "available_mcp_tools" and "selected_tools" arrays are both populated.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Tools are discovered, displayed in the UI, and present in the Raw JSON.

**Fail:**
- Any step produces an error or unexpected result.
- Tools are not loaded or not reflected in the Raw JSON.
