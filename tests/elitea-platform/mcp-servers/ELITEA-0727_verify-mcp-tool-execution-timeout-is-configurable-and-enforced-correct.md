---
id: ELITEA-0727
title: "Verify MCP tool execution timeout is configurable and enforced correctly"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp]
requirements: []
---
# ELITEA-0727: Verify MCP tool execution timeout is configurable and enforced correctly

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** MCP tool execution timeout is not configurable by users. Long-running MCP tools may time out prematurely with a hard-coded default, or conversely may hang indefinitely without a timeout. Users need the ability to set custom timeout values based on the expected execution duration of their MCP tools.

## Preconditions

User is logged into Elitea platform
At least one MCP server is configured with tools that can be executed
User has permission to configure MCP server settings
User has access to MCP management page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the MCP servers page and open the configuration/settings for an existing MCP server | MCP server configuration page loads showing all configurable settings |
| 2 | Look for a timeout configuration field (e.g., 'Execution Timeout', 'Tool Timeout', 'Request Timeout') in the server settings | A timeout configuration field is present with a default value displayed (e.g., 30 seconds, 60 seconds) |
| 3 | Verify the timeout field accepts valid numeric input. Enter a custom timeout value (e.g., 120 seconds) | Field accepts the numeric value. Input validation allows reasonable timeout values |
| 4 | Try entering invalid timeout values: 0, negative numbers, extremely large numbers (999999), non-numeric text | Invalid values are rejected with appropriate validation messages. Only positive, reasonable timeout values are accepted |
| 5 | Save the configuration with a short timeout value (e.g., 5 seconds) and execute an MCP tool that takes longer than 5 seconds | Tool execution is terminated after 5 seconds with a clear timeout error message indicating the configured limit was reached |
| 6 | Update the timeout to a longer value (e.g., 120 seconds) and re-execute the same tool | Tool is allowed to run for up to 120 seconds. If it completes within the limit, results are returned successfully |
| 7 | Verify the timeout setting persists after navigating away and returning to the MCP server configuration | Previously saved timeout value is still displayed correctly in the configuration |
| 8 | If per-tool timeout override exists, configure a different timeout for a specific tool and verify it takes precedence over the server-level timeout | Tool-level timeout overrides server-level default. Each tool respects its configured timeout independently |

## Expected Final State

Tool-level timeout overrides server-level default. Each tool respects its configured timeout independently

## Pass/Fail Criteria

PASS: Timeout field is present and configurable, valid values are saved and enforced, invalid values are rejected, and timeout errors are clearly reported
FAIL: No timeout configuration exists, configured values are not enforced, invalid values are accepted, or timeout errors provide no useful information
