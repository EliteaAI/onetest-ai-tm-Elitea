---
id: ELITEA-2864
title: "Automated: Basic interjection queuing and sequential processing"
priority: critical
type: automated
module: interjections
status: draft
execution_type: automated
tags: [feat:chat, r-2.0.6, interjection, automated, regression]
requirements: [EliteaAI/elitea_issues#6115]
automation_test_id: test_interjection_queuing_sequential
code_ref: tests/automated-full-regression-ui/chat/test_interjections.py::test_interjection_queuing_sequential
---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_interjection_queuing_sequential` |
| CI Job | `regression-ui` |

## Test Scenario

Verify that messages sent during active agent/LLM run are queued and processed sequentially.

## Automated Steps

1. Login and navigate to chat
2. Send initial message to trigger agent run
3. While agent is processing, send interjection message
4. Verify "Waiting messages · 1" indicator appears
5. Wait for initial response to complete
6. Verify interjection is processed and gets separate response
7. Assert message order in timeline

## Assertions

- Interjection queued indicator visible
- Both messages get individual responses
- FIFO order maintained
- No duplicate responses
