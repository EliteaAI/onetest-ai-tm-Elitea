---
id: ELITEA-0154
title: "Chat — Last version unpublished: card error, details blocked, chat fully non-functional"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4701]
---
# ELITEA-0154: Chat — Last version unpublished: card error, details blocked, chat fully non-functional

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the only/last published version of an agent is unpublished, an error is shown on the agent card, agent details cannot be opened, and the chat is fully non-functional — agent cannot be selected and cannot be invoked via a natural language message.

**Coverage:**
- Error displayed on agent card in Agent Studio
- Agent details panel cannot be opened
- After opening the existing chat: agent cannot be selected as a participant
- Natural language message attempting to run the agent produces no response

## Preconditions

- Logged in to {{base_url}}
- Agent "Test Publishing" has exactly one published version (V1), which has been unpublished (version reverts to Draft) — no remaining published versions
- An existing conversation with that agent and prior message history exists

## Test Data

- Agent name: "Test Publishing"
- Natural language message to attempt: "Run agent 'Test Publishing' with task: write a short story"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent Studio. Find the 'Test Publishing' agent card. | Error indicator is visible on the agent card. |
| 2 | Click the agent card to open agent details. | Agent details panel does not open. Navigation to details is blocked. |
| 3 | Navigate to the existing conversation that was using V1. | Conversation view loads. Prior message history is visible. |
| 4 | Attempt to select 'Test Publishing' via the chat participant picker. | Agent cannot be selected — no published version is available. |
| 5 | Type a natural language message referencing the agent by name (e.g., "Run agent 'Test Publishing' with task: write a short story") and send. | The agent is not invoked. |

## Expected Final State

The agent is not invoked.

## Pass/Fail Criteria

**Pass:**
- Error indicator visible on the agent card
- Agent details panel does not open
- Agent cannot be selected in the chat participant picker
- A natural language message referencing the agent should NOT trigger it.

**Fail:**
- Agent details open successfully
- Agent can be selected in the participant picker
- Any message sent triggers an agent response
