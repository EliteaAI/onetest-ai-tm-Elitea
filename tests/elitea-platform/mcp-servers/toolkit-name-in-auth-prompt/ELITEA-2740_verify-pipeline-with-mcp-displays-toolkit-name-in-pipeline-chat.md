---
id: ELITEA-2740
title: "Verify pipeline with MCP displays toolkit name in Pipeline chat section"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:pipeline]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Ability to create pipelines and add MCPs/agents

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Pipeline | Data Processing Pipeline | Pipeline with MCP toolkit |
| MCP Name | GitHub Toolkit | Remote MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/pipelines/` | Pipelines list page loads |
| 2 | Create a new Pipeline "Data Processing Pipeline" | Pipeline creation page opens |
| 3 | Add **MCP toolkit** "GitHub Toolkit" to the pipeline (do NOT click "Log in") | MCP added to pipeline, shows "Log in" button (NOT logged in) |
| 4 | Go to Right Chat part inside Pipeline | Right Chat part inside Pipeline opens |
| 5 | Send a message that requires the MCP (e.g., "Get my GitHub repositories") | Pipeline responds with authorization needed message |
| 6 | Verify the pipeline message content | Message displays "GitHub Toolkit" name and its characteristics, making it clear which MCP needs authorization |

## Alternative: Pipeline with Agent containing MCPs

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Pipeline with an **Agent** that has multiple unauthorized MCPs attached | Pipeline created with nested agent |
| 2 | Go to Right Chat part inside Pipeline | Right Chat part opens |
| 3 | Send a message that triggers the agent's MCP usage | Pipeline/Agent responds with authorization message |
| 4 | Verify the message | Message displays the specific MCP toolkit name and characteristics |

## Expected Final State

When testing a pipeline (with MCP toolkit or with agent containing MCPs) from Pipeline's chat section, the authorization message clearly identifies:
- The specific toolkit name
- Toolkit characteristics/description
- That authorization is required

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name and characteristics
- User understands which MCP in the pipeline needs authorization
- Message is clear within pipeline chat context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Toolkit characteristics are missing
