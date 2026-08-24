---
id: ELITEA-2742
title: "Verify pipeline with nested pipeline (containing agent with MCP) displays toolkit name in Pipeline chat"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:pipeline, feat:nested-agent]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Ability to create nested pipelines

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Parent Pipeline | Main Workflow | Contains nested pipeline |
| Nested Pipeline | Data Processing | Contains agent with MCP |
| Agent | GitHub Agent | Has "GitHub Toolkit" MCP (unauthorized) |
| MCP Name | GitHub Toolkit | Remote MCP (unauthorized) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/pipelines/` | Pipelines list page loads |
| 2 | Create "Main Workflow" pipeline | Parent pipeline created |
| 3 | Create "Data Processing" nested pipeline that contains "GitHub Agent" (agent has unauthorized "GitHub Toolkit" MCP) | Nested pipeline structure created |
| 4 | Add nested "Data Processing" pipeline to "Main Workflow" | Nested pipeline added to parent pipeline |
| 5 | Open "Main Workflow" pipeline and go to Right Chat part inside Pipeline | Right Chat part inside Pipeline opens |
| 6 | Send a message that triggers the nested pipeline and its agent's MCP (e.g., "Run data processing workflow") | Parent pipeline calls nested pipeline, which calls agent requiring MCP authorization |
| 7 | Verify the authorization message | Message displays "GitHub Toolkit" name and characteristics, making it clear which MCP in which nested pipeline's agent needs authorization |

## Expected Final State

When testing a pipeline with nested pipeline (containing agent with MCP) from Pipeline's chat section, the authorization message clearly identifies:
- The specific toolkit name
- Toolkit characteristics
- Which nested pipeline's agent contains the MCP requiring authorization

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name "GitHub Toolkit"
- Message includes toolkit characteristics/description
- User understands which nested pipeline's agent's MCP needs authorization
- Message is clear within pipeline chat context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Unclear which nested component's MCP needs authorization
- Toolkit characteristics are missing
