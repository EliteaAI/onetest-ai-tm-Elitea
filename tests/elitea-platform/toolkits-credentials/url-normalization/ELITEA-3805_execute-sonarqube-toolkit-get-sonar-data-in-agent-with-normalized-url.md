---
id: ELITEA-3805
title: "Execute SonarQube toolkit get_sonar_data in Agent with normalized URL"
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
- SonarQube toolkit is configured with url containing trailing slash (e.g., `https://sonar.example.com/`)
- Check Connection for SonarQube toolkit passed successfully
- User has access to Agents section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube url | `https://sonar.example.com/` (with trailing slash) |
| SonarQube project key | Valid project key |
| Agent name | `Test Agent - SonarQube URL Normalization` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents section | Agents page loads successfully |
| 2 | Create new agent or open existing agent | Agent configuration page opens |
| 3 | Add SonarQube toolkit to the agent | SonarQube toolkit appears in agent's available tools |
| 4 | Enable SonarQube tool (e.g., "get_sonar_data") | Tool is enabled |
| 5 | Save the agent configuration | Agent saved successfully |
| 6 | Open the agent in Chat or execution mode | Agent is ready |
| 7 | Send a prompt that triggers SonarQube tool execution (e.g., "Get SonarQube data for project X") | Agent processes the request |
| 8 | Observe agent execution and SonarQube tool call | SonarQube tool executes without errors |
| 9 | Verify tool response contains valid SonarQube data | Tool returns expected data (metrics, issues, etc.) |
| 10 | Check for any URL-related errors | No errors related to malformed URLs |
| 11 | Verify API path concatenation is correct | URL + relative path = proper endpoint (no double slashes like `https://sonar.example.com//api/...`) |
| 12 | Execute another SonarQube tool call from the same agent | Second tool call also succeeds |

## Expected Final State

- Agent successfully executes SonarQube toolkit tools with normalized url
- SonarQube API paths are properly concatenated (normalized url + relative path)
- get_sonar_data tool works correctly despite url having trailing slash
- Agent workflow completes without URL-related errors

## Pass/Fail Criteria

**Pass:**
- SonarQube toolkit tools execute successfully in agent workflow
- Valid data is returned from SonarQube API calls
- No URL-related errors in response or logs
- API endpoint construction produces valid URLs: `https://sonar.example.com/api/...` (not `https://sonar.example.com//api/...`)
- URL + relative path concatenation works correctly

**Fail:**
- SonarQube toolkit tool execution fails with URL-related errors
- Malformed URLs with double slashes are generated in API calls
- get_sonar_data fails due to trailing slash in url
- Agent workflow is interrupted by toolkit errors
