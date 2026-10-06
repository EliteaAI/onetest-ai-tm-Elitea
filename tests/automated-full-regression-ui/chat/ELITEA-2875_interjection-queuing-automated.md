---
id: ELITEA-2875
title: "Automated: Basic interjection queuing and sequential processing"
priority: critical
type: automated
module: interjections
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, regression]
requirements: [EliteaAI/elitea_issues#6115]
---

# ELITEA-2875: Basic interjection queuing and sequential processing

**Module:** interjections · **Priority:** critical · **Type:** automated

**Objective:** Verify that messages sent during active agent/LLM run are queued and processed sequentially.

---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_interjection_queuing_sequential` |
| CI Job | `regression-ui` |

---

## Preconditions

- User is logged in to the Elitea platform.
- Chat interface is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login and navigate to chat | Chat interface is displayed |
| 2 | Send initial message to trigger agent run | Agent starts processing the message |
| 3 | While agent is processing, send interjection message | Interjection is sent successfully |
| 4 | Verify "Waiting messages · 1" indicator appears | Queue indicator shows "Waiting messages · 1" |
| 5 | Wait for initial response to complete | First agent response completes successfully |
| 6 | Verify interjection is processed and gets separate response | Interjection receives its own agent response |
| 7 | Assert message order in timeline | Messages appear in FIFO order: initial message → response → interjection → response |

---

## Expected Final State

Both messages receive individual responses, queue indicator appears and clears correctly, and FIFO order is maintained throughout.

---

## Pass/Fail Criteria

**Pass:**
- Interjection queued indicator visible during processing
- Both messages get individual responses
- FIFO order maintained
- No duplicate responses

**Fail:**
- Queue indicator does not appear
- Interjection processed out of order
- Messages do not receive separate responses
- Duplicate or missing responses
