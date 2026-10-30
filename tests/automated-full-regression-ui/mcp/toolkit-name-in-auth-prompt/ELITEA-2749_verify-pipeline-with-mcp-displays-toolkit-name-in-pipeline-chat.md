---
id: ELITEA-2749
title: "Pipeline Execution Contexts — MCP Authorization Messages"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:pipeline, feat:nested-agent, feat:chat]
requirements: [EliteaAI/elitea_issues#5637]
---

# ELITEA-2749: Pipeline Execution Contexts — MCP Authorization Messages

**Module:** mcp-servers · **Priority:** high · **Type:** functional

**Objective:** Verify that MCP authorization messages correctly display toolkit name and characteristics across all pipeline execution contexts: direct pipeline from Pipeline page, pipeline from Chat page, nested pipeline from Pipeline page, and nested pipeline from Chat page.

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Ability to create pipelines, add MCPs/agents, and create nested pipelines

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Simple Pipeline | API Integration Pipeline | Has "GitHub Toolkit" MCP (unauthorized) |
| Parent Pipeline | Main Workflow | Contains nested pipeline |
| Nested Pipeline | GitHub Operations | Contains agent with MCP |
| Agent in Nested | GitHub Agent | Has "GitHub Toolkit" MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **PIPELINE FROM PIPELINE PAGE** | | |
| 1 | Navigate to `{{base_url}}/app/pipelines/` | Pipelines list page loads |
| 2 | Open "API Integration Pipeline" (has unauthorized "GitHub Toolkit" MCP) | Pipeline page loads, MCP shows "Log in" button (NOT logged in) |
| 3 | Go to Right Chat part inside Pipeline | Right Chat part inside Pipeline opens |
| 4 | Send a message requiring the MCP (e.g., "Get my GitHub repositories") | Pipeline responds with authorization needed message |
| 5 | Verify the pipeline message | Message displays "GitHub Toolkit" name and characteristics; user understands which MCP needs authorization |
| **PIPELINE FROM CHAT PAGE** | | |
| 6 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 7 | Start a new conversation | Chat conversation ready |
| 8 | Add "API Integration Pipeline" to the chat | Pipeline added to conversation as participant |
| 9 | Send a message triggering the pipeline and requiring MCP (e.g., "Run pipeline to get GitHub data") | Pipeline executes and responds with authorization needed message |
| 10 | Verify authorization message in chat | Message displays "GitHub Toolkit" name and characteristics within chat context |
| 11 | Verify message formatting | Message is clear and readable within chat interface |
| **NESTED PIPELINE FROM PIPELINE PAGE** | | |
| 12 | Navigate back to `{{base_url}}/app/pipelines/` | Pipelines list page loads |
| 13 | Open "Main Workflow" pipeline (contains nested "GitHub Operations" pipeline with agent having unauthorized MCP) | Parent pipeline page loads |
| 14 | Go to Right Chat part inside Pipeline | Right Chat part opens |
| 15 | Send a message triggering the nested pipeline flow (e.g., "Run main workflow") | Parent pipeline calls nested pipeline, which calls agent requiring MCP authorization |
| 16 | Verify the authorization message | Message displays "GitHub Toolkit" name and characteristics; user understands which nested pipeline's agent's MCP needs authorization |
| 17 | Verify nested context is clear | Message indicates which nested component requires authorization |
| **NESTED PIPELINE FROM CHAT PAGE** | | |
| 18 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 19 | Start a new conversation | Chat conversation ready |
| 20 | Add "Main Workflow" pipeline to chat (has nested pipeline with agent containing unauthorized MCP) | Parent pipeline added to conversation |
| 21 | Send a message triggering nested pipeline flow (e.g., "Run the main workflow") | Parent pipeline executes, calls nested pipeline, which calls agent requiring MCP authorization |
| 22 | Verify authorization message in chat | Message displays "GitHub Toolkit" name and characteristics within chat context |
| 23 | Verify user can identify nested component | Message clearly indicates which nested pipeline's agent's MCP needs authorization |

## Expected Final State

MCP authorization messages consistently display toolkit name and characteristics across all pipeline execution contexts:
- Pipeline from Pipeline page
- Pipeline from Chat page
- Nested pipeline from Pipeline page
- Nested pipeline from Chat page

## Pass/Fail Criteria

**Pass:**
- Pipeline from Pipeline page: shows toolkit name "GitHub Toolkit" with characteristics
- Pipeline from Chat: shows toolkit name "GitHub Toolkit" with characteristics in chat context
- Nested pipeline from Pipeline page: shows toolkit name with nested context clear
- Nested pipeline from Chat: shows toolkit name with nested context in chat
- All messages allow user to identify which specific MCP needs authorization
- Message formatting is consistent and readable across all contexts

**Fail:**
- Any message doesn't show toolkit name
- Generic messages without identifying the specific MCP
- User cannot determine which MCP (or which nested component's MCP) needs authorization
- Toolkit characteristics are missing
- Message formatting unclear or inconsistent between contexts
- Nested pipeline context not clear in authorization messages

## Notes

**Source functional tests:** ELITEA-2749 (Pipeline from Pipeline page), ELITEA-2750 (Pipeline from Chat), ELITEA-2751 (Nested pipeline from Pipeline page), ELITEA-2752 (Nested pipeline from Chat)

**Regression rationale:** Consolidates all pipeline execution contexts into one comprehensive journey. All four tests validate the same authorization message rendering logic in different UI contexts (Pipeline page vs Chat) and entity structures (direct pipeline vs nested pipeline with agent). Testing these together ensures MCP authorization messages are consistent across all pipeline entry points while validating nested pipeline MCP propagation.

**Selected checkpoints:** Pipeline from Pipeline page shows toolkit name; pipeline from Chat shows toolkit name in chat context; nested pipeline from Pipeline page shows toolkit name with nested context; nested pipeline from Chat shows toolkit name with nested context in chat; all messages display characteristics; user can identify which MCP needs authorization in all contexts including nested structures.
