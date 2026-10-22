---
id: ELITEA-3800
title: "Execute Salesforce toolkit in Agent workflow with normalized URL"
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
- Salesforce toolkit is configured with base_url containing trailing slash (e.g., `https://company.my.salesforce.com/`)
- Check Connection for Salesforce toolkit passed successfully
- User has access to Agents section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Salesforce base_url | `https://company.my.salesforce.com/` (with trailing slash) |
| Salesforce object | Valid object name (e.g., `Account`, `Contact`) |
| Agent name | `Test Agent - Salesforce URL Normalization` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents section | Agents page loads successfully |
| 2 | Create new agent or open existing agent | Agent configuration page opens |
| 3 | Add Salesforce toolkit to the agent | Salesforce toolkit appears in agent's available tools |
| 4 | Enable Salesforce tools (e.g., "Query records", "Get object metadata") | Tools are enabled |
| 5 | Save the agent configuration | Agent saved successfully |
| 6 | Open the agent in Chat or execution mode | Agent is ready |
| 7 | Send a prompt that triggers Salesforce tool execution (e.g., "Query Account records") | Agent processes the request |
| 8 | Observe agent execution and Salesforce tool call | Salesforce tool executes without errors |
| 9 | Verify tool response contains valid Salesforce data | Tool returns expected data (records or metadata) |
| 10 | Check for any URL-related errors | No errors related to malformed URLs or OAuth issues |
| 11 | Verify Salesforce REST API paths are correct | API paths properly constructed (no double slashes) |
| 12 | Execute another Salesforce tool call from the same agent | Second tool call also succeeds |

## Expected Final State

- Agent successfully executes Salesforce toolkit tools with normalized base_url
- Salesforce REST API calls use properly formatted URLs
- OAuth authentication works correctly with normalized URL
- Agent workflow completes without URL-related errors

## Pass/Fail Criteria

**Pass:**
- Salesforce toolkit tools execute successfully in agent workflow
- Valid data is returned from Salesforce API calls
- No URL-related errors in response or logs
- REST API paths are properly formatted
- OAuth flow works correctly with normalized URL

**Fail:**
- Salesforce toolkit tool execution fails with URL-related errors
- Malformed REST API URLs are generated
- OAuth authentication fails due to trailing slash
- Agent workflow is interrupted by toolkit errors
