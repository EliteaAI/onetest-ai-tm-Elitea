---
id: ELITEA-3638
title: "Analytics — MCP Tool Calls Counting"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, mcp, tools, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3638: Analytics — MCP Tool Calls Counting

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that MCP tool calls are counted accurately in the Analytics Tools tab.

**Coverage:**
- TOOL RUNS KPI increments per tool call
- Tool Details table tracks individual tool calls
- Multiple calls to same tool are counted separately

## Preconditions

- Logged in to {{base_url}}
- MCP server configured with tools (e.g., list_files, read_file, read_multiple_files)
- Agent with MCP tools enabled
- User has access to Settings > Analytics > Tools tab

## Test Data

| Field | Value |
|-------|-------|
| Tool 1 | list_files |
| Tool 2 | read_file |
| Tool 3 | read_multiple_files |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Overview tab | Note TOOL RUNS KPI value (e.g., N) |
| 2 | Navigate to Settings > Analytics > Tools tab | Note current CALLS for each tool |
| 3 | Execute an agent that uses list_files tool | Agent calls list_files tool |
| 4 | Execute an agent that uses read_file tool | Agent calls read_file tool |
| 5 | Navigate to Analytics > Overview tab | TOOL RUNS = N + 2 (or more if multiple calls) |
| 6 | Navigate to Analytics > Tools tab | Tool Details table updated |
| 7 | Verify list_files row: CALLS incremented | Call count accurate |
| 8 | Verify read_file row: CALLS incremented | Call count accurate |
| 9 | Check "Most Popular Tools" chart | Tools with most calls appear in chart |

## Expected Final State

Each tool call is tracked individually. TOOL RUNS KPI equals sum of all tool CALLS. Tools appear in popularity chart based on usage.

## Pass/Fail Criteria

**Pass:**
- TOOL RUNS KPI = Sum(Tool CALLS)
- Each tool shows accurate call count
- Chart reflects actual usage ranking

**Fail:**
- Tool calls not counted
- Calls attributed to wrong tool
- Chart does not match table data
