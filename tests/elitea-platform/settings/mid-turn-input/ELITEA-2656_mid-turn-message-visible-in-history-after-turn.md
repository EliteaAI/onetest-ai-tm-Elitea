---
id: ELITEA-2656
title: "Verify mid-turn message visible in conversation history after turn completes"
priority: critical
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
- User has completed a mid-turn interaction (sent message during agent turn)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Complete a turn with mid-turn input (as per ELITEA-2656) | Turn completes with mid-turn interaction |
| 2 | Scroll through conversation history | All messages are visible |
| 3 | Locate the original user message | Original message is displayed |
| 4 | Locate the mid-turn interjection message | Mid-turn message is visible with "sent while running" label |
| 5 | Verify message sequence | Messages appear in chronological order: original → mid-turn → agent response |

## Expected Final State

Conversation history correctly displays both the original message and mid-turn interjection with appropriate labeling and in correct chronological sequence.

## Pass/Fail Criteria

**Pass:**
- Original message is visible
- Mid-turn message is visible with "sent while running" label
- Messages are in correct chronological order

**Fail:**
- Mid-turn message is missing
- Label is missing or incorrect
- Message order is wrong
