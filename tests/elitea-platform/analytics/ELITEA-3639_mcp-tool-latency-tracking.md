---
id: ELITEA-3639
title: "Analytics — MCP Tool Latency Tracking"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, mcp, tools, latency, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3639: Analytics — MCP Tool Latency Tracking

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that MCP tool call latency is tracked and displayed accurately.

**Coverage:**
- AVG LATENCY is calculated per tool
- Latency is displayed in appropriate units (ms for fast, s for slow)
- Latency reflects actual tool execution time

## Preconditions

- Logged in to {{base_url}}
- MCP tools with varying execution times available
- User has access to Analytics > Tools tab

## Test Data

| Field | Value |
|-------|-------|
| Fast Tool | list_files (expected ~200ms) |
| Slow Tool | read_multiple_files (expected ~seconds) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Tools tab | Tool Details table visible |
| 2 | Execute agent that calls list_files tool | Tool executes quickly |
| 3 | Navigate to Analytics > Tools tab | list_files row shows AVG LATENCY |
| 4 | Verify latency format for fast tool | Displayed in milliseconds (e.g., 216ms) |
| 5 | Execute agent that calls read_multiple_files with several files | Tool takes longer to execute |
| 6 | Navigate to Analytics > Tools tab | read_multiple_files shows AVG LATENCY |
| 7 | Verify latency format for slower tool | Displayed in seconds if >1s (e.g., 90.6s) |
| 8 | Execute list_files again (to test averaging) | Second call completes |
| 9 | Verify AVG LATENCY updated | Average of both calls displayed |

## Expected Final State

Each tool shows accurate average latency. Fast tools show ms, slow tools show s. Multiple calls are averaged correctly.

## Pass/Fail Criteria

**Pass:**
- Latency tracked for each tool call
- AVG LATENCY = average of all calls
- Appropriate unit formatting (ms/s)

**Fail:**
- Latency not tracked
- Incorrect average calculation
- Wrong unit display
