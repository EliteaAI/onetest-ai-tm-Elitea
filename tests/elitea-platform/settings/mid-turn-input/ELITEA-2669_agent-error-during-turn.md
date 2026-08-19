---
id: ELITEA-2669
title: "Verify mid-turn input handling when agent encounters error"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- Agent configured with toolkit that may fail (e.g., external API)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger agent action that may cause an error | Agent starts |
| 2 | Send mid-turn message while agent is processing | Mid-turn message sent |
| 3 | Agent encounters error | Error is displayed |
| 4 | Verify mid-turn message handling | Message is preserved in history or handled gracefully |
| 5 | Verify conversation can continue | New messages can be sent |

## Expected Final State

When agent errors occur with pending mid-turn input, the input is handled gracefully and conversation can continue.

## Pass/Fail Criteria

**Pass:**
- Error displayed properly
- Mid-turn message preserved
- Conversation recoverable

**Fail:**
- Mid-turn message lost
- Conversation corrupted
- Cannot continue chatting
