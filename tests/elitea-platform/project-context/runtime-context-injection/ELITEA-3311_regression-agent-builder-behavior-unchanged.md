---
id: ELITEA-3311
title: "Agent Builder continues to receive context as before with no regression"
priority: high
type: regression
module: agents
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, agent-builder, regression]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3311: Agent Builder continues to receive context as before with no regression

## Preconditions

- User is logged in to `{{base_url}}`
- Agent & Pipeline Builder module is enabled
- User has successfully created agents via chat before (baseline behavior known)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Agent & Pipeline Builder in Chat Modules | Module is enabled |
| 2 | Send: "Create an agent called 'Support Bot' that helps users troubleshoot common issues" | Assistant proceeds with agent creation |
| 3 | If clarifying questions are asked (Ask User flow), answer them | Flow continues as expected |
| 4 | Verify the agent is created successfully | Agent chip/link appears in chat response |
| 5 | Click the agent chip to open the agent | Agent opens correctly in configuration/Canvas mode |
| 6 | Navigate to Agents list and verify the agent appears in current project | Agent is listed in the correct project |
| 7 | Test the created agent by starting a conversation | Agent responds as expected |

## Expected Final State

Agent Builder behavior is completely unchanged by the runtime_context enhancement to Project Context Builder and Skill Builder. The existing context injection for Agent Builder continues to work.

## Pass/Fail Criteria

**Pass:**
- Agent creation completes successfully as before
- Agent appears in the correct project
- All existing Agent Builder features work correctly
- No changes to Agent Builder user experience

**Fail:**
- Agent creation behavior changed
- Agent appears in wrong project
- New errors or regressions in Agent Builder
- Context injection broken for Agent Builder
