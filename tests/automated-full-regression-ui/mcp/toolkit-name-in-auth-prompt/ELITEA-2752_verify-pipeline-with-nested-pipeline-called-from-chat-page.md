---
id: ELITEA-2743
title: "Verify pipeline with nested pipeline displays toolkit name when called from Chat page"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:pipeline, feat:nested-agent, feat:chat]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Pipeline with nested pipeline (containing agent with MCP) exists

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Parent Pipeline | Integration Workflow | Contains nested pipeline |
| Nested Pipeline | GitHub Operations | Contains agent with MCP |
| Agent | GitHub Agent | Has "GitHub Toolkit" MCP (unauthorized) |
| MCP Name | GitHub Toolkit | Remote MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat/` | Chat page loads |
| 2 | Start a new conversation | Chat conversation ready |
| 3 | Add "Integration Workflow" pipeline to the chat (this pipeline has nested "GitHub Operations" pipeline with agent containing unauthorized MCP) | Parent pipeline added to conversation |
| 4 | Send a message that triggers the nested pipeline flow (e.g., "Run integration workflow") | Parent pipeline executes, calls nested pipeline, which calls agent requiring MCP authorization |
| 5 | Verify the authorization message in chat | Message displays "GitHub Toolkit" name and characteristics, making it clear which MCP in which nested pipeline's agent needs authorization |

## Expected Final State

When calling a pipeline from Chat page that has nested pipeline (containing agent with MCP), the authorization message clearly identifies:
- The specific toolkit name
- Toolkit characteristics
- Which nested pipeline's agent contains the MCP requiring authorization

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name "GitHub Toolkit"
- Message includes toolkit characteristics/description
- User understands which nested pipeline's agent's MCP needs authorization
- Message formatting is clear within chat context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Unclear which nested component's MCP needs authorization
- Toolkit characteristics are missing
