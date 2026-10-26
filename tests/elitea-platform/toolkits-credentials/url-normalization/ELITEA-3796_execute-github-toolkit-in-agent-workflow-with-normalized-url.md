---
id: ELITEA-3796
title: "Execute GitHub toolkit in Agent workflow with normalized URL"
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
- GitHub toolkit is configured with base_url containing trailing slash (e.g., `https://api.github.com`)
- Check Connection for GitHub toolkit passed successfully
- User has access to Agents section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| GitHub base_url | `https://api.github.com//` (with trailing slash) |
| GitHub repository | Valid repository name (e.g., `owner/repo`) |
| Agent name | `Test Agent - GitHub URL Normalization` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents section | Agents page loads successfully |
| 2 | Create new agent or open existing agent | Agent configuration page opens |
| 3 | Add GitHub toolkit to the agent | GitHub toolkit appears in agent's available tools |
| 4 | Enable GitHub tools (e.g., "List repositories", "Get file content") | Tools are enabled |
| 5 | Save the agent configuration | Agent saved successfully |
| 6 | Open the agent in Chat or execution mode | Agent is ready |
| 7 | Send a prompt that triggers GitHub tool execution (e.g., "List repositories for owner X") | Agent processes the request |
| 8 | Observe agent execution and GitHub tool call | GitHub tool executes without errors |
| 9 | Verify tool response contains valid GitHub data | Tool returns expected data |
| 10 | Check for any URL-related errors | No errors related to malformed URLs |
| 11 | Verify GitHub API endpoint construction | Endpoints are properly formatted (no double slashes like `https://github.example.com/api/v3//repos/...`) |
| 12 | Execute another GitHub tool call from the same agent | Second tool call also succeeds |

## Expected Final State

- Agent successfully executes GitHub toolkit tools with normalized base_url
- GitHub API endpoints are constructed correctly (no double slashes)
- GitHub client initializes correctly despite base_url having trailing slash
- Agent workflow completes without URL-related errors

## Pass/Fail Criteria

**Pass:**
- GitHub toolkit tools execute successfully in agent workflow
- Valid data is returned from GitHub API calls
- No URL-related errors in response or logs
- API endpoint URLs are properly formatted
- GitHub client initialization works with normalized URL

**Fail:**
- GitHub toolkit tool execution fails with URL-related errors
- Malformed API endpoint URLs are generated
- GitHub client fails to initialize due to trailing slash
- Agent workflow is interrupted by toolkit errors
