---
id: ELITEA-4254
title: Send message to Catalog skill participant in chat
priority: critical
type: regression
module: elitea-platform
status: draft
execution_type: manual
tags: [feat:skills, skill-run, catalog, chat, messaging, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4254: Send message to Catalog skill participant in chat (Regression)

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that user can send messages to Catalog skill participant in chat and receive appropriate responses.

**Coverage:**
- Message sends successfully
- Skill responds based on instructions
- Response appears in chat thread
- Conversation flows like normal chat

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open (e.g., "animal-joke")
- Chat input field is active

## Test Data

- Test message: "Hello, tell me a joke"
- Expected: Skill responds with a joke based on its instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In chat with Catalog skill participant, type message: "Hello, tell me a joke" | Message appears in input field |
| 2 | Click Send button or press Enter | Message submits successfully |
| 3 | Observe the chat thread | User message appears in chat with timestamp |
| 4 | Wait for skill response (streaming) | Loading indicator shows (if applicable) |
| 5 | Observe the skill's response | Skill responds with a joke about animals (based on "animal-joke" skill instructions) |
| 6 | Verify response appears in chat thread | Response appears below user message with skill icon/name |
| 7 | Check response quality | Response is relevant, follows skill's instructions, and is properly formatted |
| 8 | Verify conversation flow | Chat behaves like normal chat with agent/assistant |

## Expected Final State

User message sent successfully; skill responds appropriately based on instructions; conversation flows naturally.

## Pass/Fail Criteria

**Pass:** Message sends, skill responds with appropriate content based on instructions, response appears in chat.

**Fail:** Message doesn't send, no response received, or response is incorrect/not based on skill instructions.
