---
id: ELITEA-0387
title: "Not Published Agent in Chat — Switch Version Without LLM Override Error"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4937]
---
# ELITEA-0387: Not Published Agent in Chat — Switch Version Without LLM Override Error

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that switching a not published agent's version from the chat UI does not trigger the spurious "LLM settings override" error and that the version change actually applies.

**Coverage:**
- Not published agent added to a new chat
- Version switched to a non-default version from the chat UI
- No LLM override error appears; version change is applied and persists after sending a message

## Preconditions

- Logged in to {{base_url}}
- A not published agent with at least 2 saved versions available (V1, V2)
- Chrome or Firefox, latest stable

## Test Data

- Agent: any not published agent with V1 and V2 saved versions
- Chat: new chat
- Message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new chat. | Empty chat opens. |
| 2 | Add the not published agent to the chat. | Agent is added. Version selector shows the default version. |
| 3 | Open the version selector in the chat UI and switch to a non-default version (e.g. V1). | V1 is selected. No error toast appears. Version selector shows V1 as active. |
| 4 | Send any message (e.g. `Hello`). | Agent responds using V1. Version selector still shows V1. |

## Expected Final State

Agent responds using V1. Version selector still shows V1.

## Pass/Fail Criteria

**Pass:**
- Version switches successfully; no LLM override error appears at any point
- Version selector reflects the newly selected version and does not revert

**Fail:**
- The error "LLM settings override is only allowed for published agents from agent studio" appears after switching the version
- Version reverts to the default after switching or after sending a message
