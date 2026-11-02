---
id: ELITEA-3792
title: "Execute Jira toolkit in Agent workflow with normalized URL"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Jira toolkit is configured with base_url containing trailing slash (e.g., `https://jira.example.com/`)
- Check Connection for Jira toolkit passed successfully (URL normalized)
- User has access to Agents section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url | `https://jira.example.com/` (with trailing slash) |
| Jira project key | Valid project key (e.g., `TEST`) |
| Agent name | `Test Agent - Jira URL Normalization` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents section | Agents page loads successfully |
| 2 | Click "Create Agent" or open existing agent | Agent configuration page opens |
| 3 | Add Jira toolkit to the agent | Jira toolkit appears in agent's available tools |
| 4 | Enable at least one Jira tool (e.g., "Search Issues" or "Get Issue") | Tool is enabled and visible in agent configuration |
| 5 | Save the agent configuration | Agent saved successfully |
| 6 | Open the agent in Chat or execution mode | Agent is ready for interaction |
| 7 | Send a prompt that triggers Jira tool execution (e.g., "Search for issues in project TEST") | Agent processes the request |
| 8 | Observe agent execution and Jira tool call | Jira tool executes without errors |
| 9 | Verify tool response contains valid Jira data | Tool returns expected data (issues list or issue details) |
| 10 | Check for any URL-related errors in response or logs | No errors related to malformed URLs or double slashes |
| 11 | Verify Jira client initialization succeeded with normalized URL | Client initialized correctly without URL format issues |
| 12 | Execute another Jira tool call from the same agent session | Second tool call also succeeds |

## Expected Final State

- Agent successfully executes Jira toolkit tools with normalized base_url
- Jira API calls are constructed with properly formatted URLs (no double slashes)
- Jira client initializes correctly despite original base_url having trailing slash
- Agent workflow completes without URL-related errors

## Pass/Fail Criteria

**Pass:**
- Jira toolkit tools execute successfully in agent workflow
- Valid data is returned from Jira API calls
- No URL-related errors appear in response or logs
- API endpoint construction produces valid URLs (no double slashes like `https://jira.example.com//rest/api/...`)
- Jira client initialization works correctly with normalized URL

**Fail:**
- Jira toolkit tool execution fails with URL-related errors
- Malformed URLs with double slashes are generated
- Jira client fails to initialize due to trailing slash in base_url
- Agent workflow is interrupted by toolkit errors
