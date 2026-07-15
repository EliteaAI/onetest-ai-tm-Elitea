---
id: ELITEA-2182
title: "Chat – Stop Button Appears During Response Generation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2182: Chat – Stop Button Appears During Response Generation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the orange stop button appears during generation and cancels the response when clicked.

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
| 2 | Verify orange square stop icon appears on far right of bottom input bar | Stop button visible |
| 3 | Click the orange stop button | Response generation stops immediately |
| 4 | Verify no further text streams after clicking stop | Streaming stopped |
| 5 | Verify stop button disappears and default input bar restored | Normal input bar visible |
| 6 | Verify input field is active and editable again | Input field active |

---

## Expected Final State

Stop button cancels generation; input bar restored.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Stop button works; generation cancelled; input restored.

**Fail:**
- Any step produces an error or unexpected result.
- Stop button not visible or fails to stop generation.
