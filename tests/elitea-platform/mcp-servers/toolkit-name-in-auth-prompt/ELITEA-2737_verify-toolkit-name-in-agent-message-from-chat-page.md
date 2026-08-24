---
id: ELITEA-2737
title: "Verify toolkit name in agent authorization message from Chat page"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:chat]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Agent with unauthorized MCP(s) exists

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | Test Agent with MCP |
| MCP Name | GitHub Toolkit |
| MCP Type | Remote MCP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 2 | Start a new conversation or open existing one | Chat conversation ready |
| 3 | Add the Agent "Test Agent with MCP" to the chat (agent has attached **unauthorized** "GitHub Toolkit") | Agent added to conversation as participant |
| 4 | Send a message to the agent that requires the MCP (e.g., "@Test Agent get my GitHub repos") | Agent responds with authorization needed message |
| 5 | Verify the agent message content | Message displays the toolkit name "GitHub Toolkit" and its characteristics, making it clear which specific MCP needs authorization |

## Expected Final State

When using an agent from Chat page, the agent's authorization message clearly identifies:
- The specific toolkit name
- Toolkit characteristics/description
- That authorization is required

## Pass/Fail Criteria

**Pass:**
- Agent message shows toolkit name "GitHub Toolkit"
- Message includes toolkit characteristics/description
- User can clearly identify which MCP needs authorization
- Message formatting is clear and readable within chat context

**Fail:**
- Agent message doesn't show toolkit name
- Agent shows generic message without identifying the specific MCP
- Toolkit characteristics are missing
- User cannot determine which MCP needs authorization
