---
id: ELITEA-2748
title: "Verify nested agent with MCP displays toolkit name from Chat page"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:nested-agent, feat:chat]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Parent agent with nested agent exists
- Nested agent has unauthorized MCP(s)

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Parent Agent | Orchestrator Agent | Main agent used from chat |
| Nested Agent | Jira Agent | Has "Atlassina remote toolkit" MCP (unauthorized) |
| MCP Name | Atlassina remote toolkit | Remote MCP for Jira |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 2 | Start a new conversation | Chat conversation ready |
| 3 | Add "Orchestrator Agent" to the chat (this agent has "Jira Agent" as nested agent with unauthorized MCP) | Parent agent added to conversation |
| 4 | Send a message that requires the nested agent's MCP (e.g., "@Orchestrator use Jira Agent to get my tasks") | Parent agent calls nested agent, which responds with authorization needed message |
| 5 | Verify the authorization message in chat | Message displays "Atlassina remote toolkit" name and characteristics, making it clear which MCP needs authorization |

## Expected Final State

When using a parent agent from Chat that calls a nested agent requiring MCP authorization, the message clearly identifies:
- The specific toolkit name
- Toolkit characteristics
- Which nested agent requires the authorization

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name "Atlassina remote toolkit"
- Message includes toolkit characteristics/description
- User understands which nested agent's MCP needs authorization
- Message formatting is clear within chat context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Unclear which nested agent's MCP needs authorization
- Toolkit characteristics are missing
