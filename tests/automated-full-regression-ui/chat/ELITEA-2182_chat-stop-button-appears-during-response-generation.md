---
id: ELITEA-2182
title: "Chat – Stop Button Appears During Response Generation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2182: Chat – Stop Button Appears During Response Generation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the stop button appears while the sub-agent/thinking phase is running and cancels the response when clicked. Updated per issue #5196: the stop button is only relevant during the "thinking"/sub-agent phase — once final response text has begun streaming, there is nothing left to interrupt and the stop control is no longer expected to remain available.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | generate a poem |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type 'generate a poem' and click Send | User message appears; generation starts |
| 2 | Verify stop icon appears on far right of bottom input bar as soon as thinking/sub-agent steps begin | Stop button visible during thinking/sub-agent phase |
| 3 | Click the stop button while thinking/sub-agent steps are still in progress | Response generation stops immediately |
| 4 | Verify no further text streams after clicking stop | Streaming stopped |
| 5 | Verify stop button disappears and default input bar restored | Normal input bar visible |
| 6 | Verify input field is active and editable again | Input field active |
| 7 | Verify input field now contains the exact original message text ("generate a poem") | Input restored with the exact original prompt, not empty |

---

## Expected Final State

Stop button cancels generation during the thinking phase; input bar restored with the exact original message.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Stop button works during thinking phase; generation cancelled; input restored with exact original text.

**Fail:**
- Any step produces an error or unexpected result.
- Stop button not visible during thinking phase, fails to stop generation, or input is not restored with the exact original text.
