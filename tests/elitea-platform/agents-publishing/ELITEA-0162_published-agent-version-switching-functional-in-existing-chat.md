---
id: ELITEA-0162
title: "Published Agent Version Switching Functional in Existing Chat"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, feat:agents, feat:chat, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4693]
---
# ELITEA-0162: Published Agent Version Switching Functional in Existing Chat

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the published agent version selector is fully functional in an existing chat that already contains prior messages, and that the user can freely switch between all published versions.

**Coverage:**
- Agent version defaults to latest when added to an existing chat
- Switching to a non-latest version (V2 out of 3) is applied correctly in an existing chat
- Switching to a second non-latest version (V1) is applied correctly
- The selected version is used for requests sent in the existing chat
- Version selector is not locked, greyed out, or non-functional due to existing message history

## Preconditions

- Logged in to {{base_url}}
- A published agent with at least 3 published versions exists (V1 oldest, V2 middle/non-latest, V3 latest/default)
- An existing chat conversation with at least one prior message exchange (sent and received) is available
- Chrome or Firefox, latest stable version

## Test Data

- Agent name: `test-published-agent` (with V1, V2, V3 published; V3 is latest/default)
- V1: oldest published version
- V2: middle published version (non-latest, non-oldest)
- V3: latest published version (default when agent is added)
- Existing chat: contains at least 1 user message and 1 agent response
- Prompt text: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing chat conversation that already contains at least one prior message exchange. | Chat history is visible with prior messages. |
| 2 | Add the published agent `test-published-agent` to the conversation. | Agent is added. Version selector shows V3 (latest) as the active/default version. Version selector is enabled and interactive. |
| 3 | Open the agent version selector and switch to V2 (the middle, non-latest version). | V2 is selected and displayed as the active version. The selector does not revert to V3. |
| 4 | Open the agent version selector again and switch to V1 (the oldest version). | V1 is selected and displayed as the active version. The selector does not revert to V3. |
| 5 | Type `Hello` in the message input and send the request. | Request is processed using V1 (the last selected version). A response is returned. Version selector still shows V1. |

## Expected Final State

Request is processed using V1 (the last selected version). A response is returned. Version selector still shows V1.

## Pass/Fail Criteria

**Pass:**
- Version selector is enabled and interactive when the agent is added to an existing chat
- Switching to V2 in step 3 is applied correctly and does not revert to V3
- Switching to V1 in step 4 is applied correctly and does not revert to V3
- Request in step 5 is processed using V1 as selected
- All 3 versions are selectable in an existing chat

**Fail:**
- Version selector is greyed out, unresponsive, or non-functional after the agent is added to an existing chat
- Selecting V2 or V1 immediately reverts back to V3 (latest) without user action
- Only V3 (the default/latest) can be used regardless of what the user selects
- Request in step 5 is processed using V3 instead of V1
