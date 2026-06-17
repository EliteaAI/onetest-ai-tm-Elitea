---
id: ELITEA-0067
title: "Regression — Chat History Preserved on Agent Page After Sub-Participant Change"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, regression, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0067: Regression — Chat History Preserved on Agent Page After Sub-Participant Change

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Regression — verify that the agent's conversation history is preserved correctly within the Agent Page after the sub-participant `chat_history` exclusion change. The agent must be able to reference previous turns in the same test session.

**Coverage:**
- Agent correctly recalls its own prior response when asked within the Test Settings session
- History within the test session is not cleared or broken by the sub-participant change
- The exclusion of `chat_history` applies only to sub-participant payloads, not to the parent session

## Preconditions

- Logged in to {{base_url}}
- An agent is open on the Agent page
- Enhancement #4790 is deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent from the Agents page. Send an initial request (e.g., 'Give me a short summary of machine learning') | Agent responds with a summary |
| 2 | In the same test session, send a follow-up: 'Repeat your previous answer' | Agent correctly recalls and restates its prior response from the test session history. No errors or context-loss behavior. |

## Expected Final State

Agent correctly recalls and restates its prior response from the test session history. No errors or context-loss behavior.

## Pass/Fail Criteria

**Pass:**
- Agent correctly recalls its prior response from the same session

**Fail:**
- Agent cannot recall the previous message (history appears lost)
- Agent returns an error or claims it has no prior context
