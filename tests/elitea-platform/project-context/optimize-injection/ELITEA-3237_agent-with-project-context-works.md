---
id: ELITEA-3237
title: "Agent with Project Context Works (Existing and New Agents)"
priority: critical
type: regression
module: project-context
status: draft
execution_type: manual
tags: [project-context, agents, r-2.0.6, eng:optimization]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Existing published agent with "Ignore Project Context" = OFF
- Project Context enabled with phrase: `QA-AGENT-CONTEXT: Agent context test`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/<project>/agents` |
| Test Phrase | `QA-AGENT-CONTEXT: Agent context test` |
| New Agent Name | `QA Test Agent - Context Validation` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to existing agent page | Agent page loads |
| 2 | Run existing agent with prompt: "What is the QA-AGENT-CONTEXT phrase?" | Agent invokes `read_project_context` tool, returns: "Agent context test" |
| 3 | Verify agent execution completes successfully | No errors, normal execution flow |
| 4 | Create new agent (any type), set "Ignore Project Context" = OFF | Agent created |
| 5 | Publish new agent | Agent published successfully |
| 6 | Run new agent with prompt: "What is the QA-AGENT-CONTEXT phrase?" | Agent invokes `read_project_context` tool, returns: "Agent context test" |
| 7 | In both agents, ask: "What is this project about?" | Both agents use Project Context info in responses |

## Expected Final State

Both existing and new agents work correctly with Project Context. Context is applied, tool call visible, responses contain context information.

## Pass/Fail Criteria

**Pass:**
- Existing agent loads and runs without errors
- New agent created and published successfully
- Project Context phrase returned correctly by both agents
- `read_project_context` tool call visible in agent execution
- Both agents use context in responses

**Fail:**
- Agent fails to load, create, or execute
- Context not applied in either agent
- Tool call not visible
- Phrase not returned
- Errors in agent execution or logs
