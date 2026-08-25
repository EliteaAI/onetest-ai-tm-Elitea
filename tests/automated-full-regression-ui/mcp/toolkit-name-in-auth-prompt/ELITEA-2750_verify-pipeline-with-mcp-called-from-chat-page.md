---
id: ELITEA-2741
title: "Verify pipeline with MCP displays toolkit name when called from Chat page"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:pipeline, feat:chat]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Pipeline with unauthorized MCP exists

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Pipeline | API Integration Pipeline | Has "GitHub Toolkit" MCP |
| MCP Name | GitHub Toolkit | Remote MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 2 | Start a new conversation | Chat conversation ready |
| 3 | Add Pipeline "API Integration Pipeline" to the chat (pipeline has unauthorized "GitHub Toolkit" MCP) | Pipeline added to conversation as participant |
| 4 | Send a message that triggers the pipeline and requires the MCP (e.g., "Run the pipeline to get GitHub data") | Pipeline executes and responds with authorization needed message |
| 5 | Verify the authorization message in chat | Message displays "GitHub Toolkit" name and characteristics, making it clear which MCP within the pipeline needs authorization |

## Expected Final State

When calling a pipeline from Chat page that requires MCP authorization, the message clearly identifies:
- The specific toolkit name
- Toolkit characteristics/description
- That the MCP is part of the pipeline

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name "GitHub Toolkit"
- Message includes toolkit characteristics/description
- User understands which MCP in the pipeline needs authorization
- Message formatting is clear within chat context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Unclear which MCP needs authorization
- Toolkit characteristics are missing
