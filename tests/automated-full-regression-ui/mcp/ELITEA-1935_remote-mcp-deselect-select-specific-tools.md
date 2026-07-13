---
id: ELITEA-1935
title: "Remote MCP — Deselect/Select Specific Tools"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1935: Remote MCP — Deselect/Select Specific Tools

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that individual tools can be removed from and added back to the "selected_tools" array via Raw JSON editing, and that the Form view reflects the updated selection.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP with discovered tools is available (e.g., "Web Search" with tavily tools).

---

## Test Data

| Field | Value |
|-------|-------|
| Tool to deselect | tavily_crawl |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP that has discovered tools (e.g., "Web Search" with tavily tools) | Detail page loads |
| 2 | Switch to Raw Json view | JSON editor is visible |
| 3 | Locate "selected_tools" array — note all tool names present | All current tool names are noted |
| 4 | Remove one tool name from "selected_tools" array (e.g., remove "tavily_crawl") | JSON editor shows array without "tavily_crawl" |
| 5 | Click Save | Operation completes successfully |
| 6 | Switch to Form view — verify the removed tool no longer active in Tools section as selected | Removed tool is no longer selected in Form view |
| 7 | Switch back to Raw Json — add the tool name back to "selected_tools" | JSON editor shows the tool re-added |
| 8 | Save — verify tool reappears | Tool is selected again in Form view |

---

## Expected Final State

The tool selection is correctly managed via Raw JSON edits, and Form view reflects the current selected_tools state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Removing and re-adding a tool name in selected_tools is reflected in the Form view.

**Fail:**
- Any step produces an error or unexpected result.
- Form view does not reflect changes made via Raw JSON.
