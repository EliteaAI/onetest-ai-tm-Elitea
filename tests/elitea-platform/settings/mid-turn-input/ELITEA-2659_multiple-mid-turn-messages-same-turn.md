---
id: ELITEA-2659
title: "Send multiple mid-turn messages during single agent run"
priority: high
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
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Write a detailed travel guide for Japan covering food, culture, and attractions" |
| Mid-turn message 1 | "Focus more on Tokyo" |
| Mid-turn message 2 | "Include budget tips" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the initial prompt to start a long agent turn | Agent begins generating |
| 2 | Send first mid-turn message | Message sent with "sent while running" indicator |
| 3 | Send second mid-turn message while agent still running | Second message also sent with indicator |
| 4 | Wait for agent to complete | Agent finishes response |
| 5 | Review agent response | Response incorporates both mid-turn inputs |
| 6 | Review conversation history | Both mid-turn messages visible in correct sequence |

## Expected Final State

Multiple mid-turn messages are accepted, delivered in sequence, and reflected in the agent's response.

## Pass/Fail Criteria

**Pass:**
- Multiple messages can be sent mid-turn
- All messages show "sent while running" indicator
- Agent processes messages in sequence
- Conversation history shows all messages correctly

**Fail:**
- Second message rejected or lost
- Messages processed out of order
- Only one message affects response
