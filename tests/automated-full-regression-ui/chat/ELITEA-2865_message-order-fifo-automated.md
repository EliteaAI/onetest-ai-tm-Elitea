---
id: ELITEA-2865
title: "Automated: FIFO message order preservation"
priority: critical
type: automated
module: interjections
status: draft
execution_type: automated
tags: [feat:chat, r-2.0.6, interjection, automated, regression]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6457]
automation_test_id: test_message_order_fifo
code_ref: tests/automated-full-regression-ui/chat/test_interjections.py::test_message_order_fifo
---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_message_order_fifo` |
| CI Job | `regression-ui` |

## Test Scenario

Verify multiple queued messages are processed in strict FIFO order.

## Automated Steps

1. Login and start long-running agent task
2. Queue 3 messages rapidly (A, B, C)
3. Verify queue count shows 3
4. Wait for all messages to process
5. Assert processing order matches send order
6. Verify each message has exactly one response

## Assertions

- Queue count increments correctly
- Processing order: A → B → C
- No message jumps ahead
- Each message = exactly one response
