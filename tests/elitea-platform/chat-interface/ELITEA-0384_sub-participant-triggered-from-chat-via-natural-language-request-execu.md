---
id: ELITEA-0384
title: "Sub-Participant Triggered from Chat via Natural Language Request Executes Correctly [Parametrized: Agent | Pipeline]"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:agents, feat:chat, sub-agent, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0384: Sub-Participant Triggered from Chat via Natural Language Request Executes Correctly [Parametrized: Agent | Pipeline]

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a user can trigger an Agent or Pipeline from the Chat page using a natural language request (e.g., "Use Agent X to do Y" or "Use Pipeline X to do Y"), and that the invoked participant executes correctly and returns a coherent result.

**Parameters:**
| # | Participant type triggered from Chat |
|---|---|
| 1 | Agent |
| 2 | Pipeline |

**Coverage (per parameter):**
- Natural language request in Chat successfully routes to the correct Agent or Pipeline
- The invoked participant executes and returns a valid result
- Chat response reflects the participant's output
- No routing errors or empty responses

## Preconditions

- Logged in to {{base_url}}
- At least one Agent and one Pipeline are configured in the project as participants in a parent agent
- Chat session is open with the parent agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat session with a parent agent that has both an Agent and a Pipeline as participants | Chat input is ready |
| 2 | Send a natural language message that requests the Agent participant: 'Use [Agent name] to [task description]' | The parent agent routes the request to the sub-agent and begins execution |
| 3 | Expand the thinking steps and inspect the participant chip that shows what was sent to the sub-agent | The input shown in the chip contains only the task context. No `chat_history` is visible in the sub-agent input. |
| 4 | Wait for the sub-agent response and verify the chat output | Sub-agent executes and returns a result. Chat response is coherent. No errors. |
| 5 | In the same or a new chat, send a natural language message that requests the Pipeline participant: 'Use [Pipeline name] to [task description]' | The parent agent routes the request to the sub-pipeline and begins execution |
| 6 | Expand the thinking steps and inspect the participant chip that shows what was sent to the sub-pipeline | The input shown in the chip contains only the task context. No `chat_history` is visible in the sub-pipeline input. |
| 7 | Wait for the sub-pipeline response and verify the chat output | Sub-pipeline executes and returns a result. Chat response is coherent. No errors. |

## Expected Final State

Sub-pipeline executes and returns a result. Chat response is coherent. No errors.

## Pass/Fail Criteria

**Pass:**
- Agent/Pipeline is correctly invoked from Chat based on the natural language request
- Execution completes and a coherent result is shown in Chat

**Fail:**
- Chat fails to route the request to the correct participant
- Agent/Pipeline is invoked but returns an error or empty result
- Chat shows an error or no response
