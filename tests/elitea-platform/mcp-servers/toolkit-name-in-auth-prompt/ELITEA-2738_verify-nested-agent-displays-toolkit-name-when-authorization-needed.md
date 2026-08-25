---
id: ELITEA-2738
title: "Verify nested agent displays toolkit name when MCP authorization is needed"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6, feat:nested-agent]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Parent agent and child (nested) agent exist
- Child agent has unauthorized MCP(s)

## Test Data

| Entity | Name | Details |
|--------|------|---------|
| Parent Agent | Orchestrator Agent | Main agent that uses nested agent |
| Nested Agent | GitHub Agent | Has "GitHub Toolkit" MCP attached (unauthorized) |
| MCP Name | GitHub Toolkit | Remote MCP, not logged in |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/agents/` | Agents list page loads |
| 2 | Open "Orchestrator Agent" configuration | Agent page loads |
| 3 | Add "GitHub Agent" as a nested agent in Tools section | "GitHub Agent" appears as nested agent (NOT logged in to its MCP) |
| 4 | Go to Right Chat part inside Agent | Right Chat part inside Agent opens |
| 5 | Send a message that requires the nested agent to use its MCP (e.g., "Use GitHub Agent to get my repos") | Parent agent calls nested agent, which responds with authorization needed message |
| 6 | Verify the authorization message | Message displays "GitHub Toolkit" name and characteristics, making it clear which MCP of which nested agent needs authorization |

## Expected Final State

When a nested agent requires MCP authorization, the message clearly identifies:
- The specific toolkit name
- Toolkit characteristics
- Which nested agent requires the authorization (if multiple nested agents exist)

## Pass/Fail Criteria

**Pass:**
- Authorization message shows toolkit name "GitHub Toolkit"
- Message includes toolkit characteristics/description
- User understands which nested agent's MCP needs authorization
- Message is clear within the parent agent's test context

**Fail:**
- Message doesn't show toolkit name
- Generic message without identifying the specific MCP
- Unclear which nested agent's MCP needs authorization
- Toolkit characteristics are missing
