---
id: ELITEA-2876
title: "Automated: FIFO message order preservation"
priority: critical
type: automated
module: interjections
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, regression]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6457]
---

# ELITEA-2876: FIFO message order preservation

**Module:** interjections · **Priority:** critical · **Type:** automated

**Objective:** Verify multiple queued messages are processed in strict FIFO order.

---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_message_order_fifo` |
| CI Job | `regression-ui` |

---

## Preconditions

- User is logged in to the Elitea platform.
- Chat interface is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Message A | "First message" |
| Message B | "Second message" |
| Message C | "Third message" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login and start long-running agent task | Agent starts processing |
| 2 | Queue message A rapidly | Message A appears in queue |
| 3 | Queue message B rapidly | Message B appears in queue |
| 4 | Queue message C rapidly | Message C appears in queue |
| 5 | Verify queue count shows 3 | Queue indicator displays "Waiting messages · 3" |
| 6 | Wait for all messages to process | All three messages receive responses sequentially |
| 7 | Assert processing order matches send order | Messages processed in order: A → B → C |
| 8 | Verify each message has exactly one response | Each message has exactly one corresponding response |

---

## Expected Final State

All messages processed in strict FIFO order (A, B, C), each with exactly one response.

---

## Pass/Fail Criteria

**Pass:**
- Queue count increments correctly to 3
- Processing order: A → B → C
- No message jumps ahead in processing
- Each message receives exactly one response

**Fail:**
- Queue count incorrect
- Processing order violated (e.g., C processed before A or B)
- Message receives duplicate or no response
