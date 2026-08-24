---
id: ELITEA-2736
title: "Verify multiple MCPs - each displays correct toolkit name in agent authorization message"
priority: critical
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Agent has multiple MCPs attached (minimum 3)
- None of the MCPs are authorized (no "Log in" clicked)

## Test Data

| MCP Name | MCP Type | Description |
|----------|----------|-------------|
| GitHub Toolkit | Remote MCP | Connect to GitHub repositories |
| Atlassian remote toolkit | Remote MCP | Connect to Atlassian/Jira |
| Epam Stuffing | Local MCP | Local development toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/agents/` | Agents list page loads |
| 2 | Open an Agent with 3+ MCPs attached, none authorized | Agent page shows all MCPs in Tools section, each with "Log in" button |
| 3 | Go to Right Chat part inside Agent | Right Chat part inside Agent opens |
| 4 | Send a message that requires the **first MCP** (e.g., "Get my GitHub repositories") | Agent responds with authorization message |
| 5 | Verify the agent message identifies the correct toolkit | Message displays "GitHub Toolkit" name and its characteristics - NOT a generic message or different MCP name |
| 6 | Send a message that requires the **second MCP** (e.g., "Get my Jira tasks") | Agent responds with authorization message |
| 7 | Verify the agent message identifies the correct toolkit | Message displays "Atlassina remote toolkit" name and its characteristics - NOT "GitHub Toolkit" or generic message |
| 8 | Send a message that requires the **third MCP** (e.g., "Use Epam Stuffing") | Agent responds with authorization message |
| 9 | Verify the agent message identifies the correct toolkit | Message displays "Epam Stuffing" name and its characteristics |

## Expected Final State

Each MCP's authorization message correctly identifies its specific toolkit name and characteristics, allowing the user to distinguish which toolkit needs authorization.

## Pass/Fail Criteria

**Pass:**
- Each MCP authorization message shows the correct, specific toolkit name
- Each message includes toolkit characteristics/description
- User can clearly distinguish between different MCPs
- No cross-contamination of toolkit names between different requests

**Fail:**
- Agent message shows wrong toolkit name
- Agent shows generic message without identifying the specific MCP
- User cannot determine which specific MCP needs authorization
- Toolkit characteristics are missing or incorrect
