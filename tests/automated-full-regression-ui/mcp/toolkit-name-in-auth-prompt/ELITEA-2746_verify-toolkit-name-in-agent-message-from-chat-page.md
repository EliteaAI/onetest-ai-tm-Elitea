---
id: ELITEA-2746
title: "Agent Execution Contexts — Chat + Nested MCP Authorization"
priority: critical
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:chat, feat:nested-agent]
requirements: [EliteaAI/elitea_issues#5637]
---

# ELITEA-2746: Agent Execution Contexts — Chat + Nested MCP Authorization

**Module:** mcp-servers · **Priority:** critical · **Type:** functional

**Objective:** Verify that MCP authorization messages correctly display toolkit name and characteristics when agents are used from Chat page and when nested agents require MCP authorization, ensuring consistent rendering across execution contexts.

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Agents with unauthorized MCP(s) exist
- Parent agent with nested agent exists

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Agent (Chat test) | Test Agent with MCP | Has "GitHub Toolkit" MCP (unauthorized) |
| Parent Agent | Orchestrator Agent | Main agent that uses nested agent |
| Nested Agent | Jira Agent | Has "Atlassian remote toolkit" MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **AGENT FROM CHAT PAGE** | | |
| 1 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 2 | Start a new conversation | Chat conversation ready |
| 3 | Add "Test Agent with MCP" to the chat (agent has unauthorized "GitHub Toolkit") | Agent added to conversation as participant |
| 4 | Send a message to the agent requiring the MCP (e.g., "@Test Agent get my GitHub repos") | Agent responds with authorization needed message |
| 5 | Verify the agent message in chat | Message displays "GitHub Toolkit" name and characteristics; user can clearly identify which MCP needs authorization |
| 6 | Verify message formatting | Message is clear and readable within chat context |
| **NESTED AGENT FROM AGENT PAGE** | | |
| 7 | Navigate to `{{base_url}}/app/agents/` | Agents list page loads |
| 8 | Open "Orchestrator Agent" configuration | Agent page loads |
| 9 | Verify "Jira Agent" is nested agent with unauthorized MCP | "Jira Agent" appears as nested agent (NOT logged in to its MCP) |
| 10 | Go to Right Chat part inside Agent | Right Chat part inside Agent opens |
| 11 | Send a message requiring nested agent's MCP (e.g., "Use Jira Agent to get my tasks") | Parent agent calls nested agent, which responds with authorization needed message |
| 12 | Verify the authorization message | Message displays "Atlassian remote toolkit" name and characteristics; clear which nested agent's MCP needs authorization |
| **NESTED AGENT FROM CHAT PAGE** | | |
| 13 | Return to `{{base_url}}/app/chat/` | Chat page loads |
| 14 | Start a new conversation | Chat conversation ready |
| 15 | Add "Orchestrator Agent" to the chat (has nested "Jira Agent" with unauthorized MCP) | Parent agent added to conversation |
| 16 | Send a message requiring nested agent's MCP (e.g., "@Orchestrator use Jira Agent to get tasks") | Parent agent calls nested agent, which responds with authorization needed message |
| 17 | Verify authorization message in chat | Message displays "Atlassian remote toolkit" name and characteristics within chat context |
| 18 | Verify user can identify which nested agent needs authorization | Message clearly indicates nested agent's MCP requirements |

## Expected Final State

MCP authorization messages consistently display toolkit name and characteristics across all agent execution contexts:
- Agent called from Chat page
- Nested agent from Agent page
- Nested agent from Chat page

## Pass/Fail Criteria

**Pass:**
- Agent from Chat: shows toolkit name "GitHub Toolkit" with characteristics
- Nested agent from Agent page: shows toolkit name "Atlassian remote toolkit" with characteristics
- Nested agent from Chat: shows toolkit name "Atlassian remote toolkit" with characteristics in chat context
- All messages are clear and allow user to identify which specific MCP needs authorization
- Message formatting is consistent and readable in both Agent page and Chat contexts

**Fail:**
- Any message doesn't show toolkit name
- Generic messages without identifying the specific MCP
- User cannot determine which MCP needs authorization
- Toolkit characteristics are missing
- Message formatting unclear or inconsistent between contexts

## Notes

**Source functional tests:** ELITEA-2746 (Agent from Chat), ELITEA-2747 (Nested agent from Agent page), ELITEA-2748 (Nested agent from Chat)

**Regression rationale:** Consolidates agent execution contexts into one coherent journey. All three tests validate the same authorization message rendering logic in different UI contexts (Chat vs Agent page) and entity structures (direct agent vs nested agent). Testing these together ensures MCP authorization messages are consistent across entry points while validating nested agent MCP propagation.

**Selected checkpoints:** Agent from Chat shows toolkit name; nested agent from Agent page shows toolkit name with nested context; nested agent from Chat shows toolkit name in chat context; all messages display characteristics; user can identify which MCP needs authorization in all contexts.
