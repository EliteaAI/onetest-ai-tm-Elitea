---
id: ELITEA-0161
title: "Published Agent Version Switching Reverts to Latest After First Request in New Chat"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, feat:agents, feat:chat, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4693]
---
# ELITEA-0161: Published Agent Version Switching Reverts to Latest After First Request in New Chat

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after switching to a non-latest published agent version in a new chat and sending a request, the selected version remains active and does not revert to the latest published version.

**Coverage:**
- Version selector defaults to the latest version when agent is added to a new chat
- Switching to a non-latest version (e.g., V2 out of 3) is applied correctly
- Sending a request does not cause an auto-revert to the latest version
- Subsequent version switches after the first request are applied correctly and remain stable
- The user-selected version is used for all subsequent requests

**Related bugs:** EliteaAI/elitea_issues#4937 (version switch triggers LLM settings override error in chat), EliteaAI/elitea_issues#4934 (LLM settings override error after save/version actions)

## Preconditions

- Logged in to {{base_url}}
- A published agent with at least 3 published versions exists (V1 oldest, V2 middle/non-latest, V3 latest/default)
- A new, empty chat conversation is available
- Chrome or Firefox, latest stable version

## Test Data

- Agent name: `test-published-agent` (with V1, V2, V3 published; V3 is latest/default)
- V1: oldest published version
- V2: middle published version (non-latest, non-oldest)
- V3: latest published version (default when agent is added)
- Prompt text: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new conversation with no messages. | Empty chat is opened with no message history. |
| 2 | Add the published agent `test-published-agent` to the conversation. | Agent is added. Version selector shows V3 (latest) as the active/default version. |
| 3 | Open the agent version selector and switch to V2 (the middle, non-latest version). | V2 is selected and displayed as the active version. The selector does not revert. |
| 4 | Type `Hello` in the message input and send the request. | Request is processed using V2. A response is returned. Version selector still shows V2 — it has not reverted to V3. |
| 5 | After the response is received, open the version selector and switch to V1. | V1 is selected and displayed as the active version. The selector does not auto-revert to V3. |
| 6 | Send a second request (e.g., `Hello again`). | Request is processed using V1 as selected in step 5. Version remains V1 after the response. |

## Expected Final State

Request is processed using V1 as selected in step 5. Version remains V1 after the response.

## Pass/Fail Criteria

**Pass:**
- Version selector remains on the user-selected version (V2) after the first request in step 4
- Switching to V1 in step 5 is applied correctly and does not revert to V3
- Second request in step 6 uses V1 as expected
- Version switching between all 3 versions works consistently before and after sending messages

**Fail:**
- After step 4, the version automatically reverts to V3 (latest) without user action
- Attempting to switch to V1 in step 5 causes an immediate snap-back to V3
- Any request uses V3 despite a different version being selected
