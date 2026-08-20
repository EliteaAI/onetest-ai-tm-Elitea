---
id: ELITEA-2661
title: "Verify mid-turn input handling and UI feedback when sent just before turn completes"
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "List 5 popular JavaScript frameworks" |
| Late mid-turn message | "Add React Native too" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt that will have a shorter response | Agent starts generating |
| 2 | Wait until agent is almost done (response nearly complete) | Agent is finishing up |
| 3 | Quickly send a mid-turn message | Message is sent |
| 4 | Observe the UI feedback immediately after sending | Message shows waiting indicator ("pending delivery" or similar) |
| 5 | Watch for UI state transition | UI changes to show either "sent while running" (picked up) or no special indicator (fell back to normal message) |
| 6 | Review conversation history | Message is visible in conversation |
| 7 | Verify message handling | Message either: (a) was delivered to current turn and agent adjusted response, OR (b) became a new message after turn completed |

## Expected Final State

Late mid-turn input is handled gracefully with clear UI feedback:
- User sees waiting state while message delivery is attempted
- UI confirms whether message was picked up or fell back to normal message
- No data loss — message is either processed in current turn or becomes next message

## Pass/Fail Criteria

**Pass:**
- UI shows waiting indicator when message sent
- UI transitions to confirmation state ("sent while running") if picked up in time
- If too late, message gracefully becomes normal message without special indicator
- Message is not silently dropped
- Conversation continues normally

**Fail:**
- Message is lost
- No UI feedback during delivery attempt
- User cannot tell what happened to their message
- Error occurs or conversation state corrupted
