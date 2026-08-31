---
id: ELITEA-2867
title: "Automated: Stop preserves queued messages"
priority: critical
type: automated
module: interjections
status: draft
execution_type: automated
tags: [feat:chat, r-2.0.6, interjection, stop, automated, regression]
requirements: [EliteaAI/elitea_issues#6115]
automation_test_id: test_stop_preserves_queue
code_ref: tests/automated-full-regression-ui/chat/test_interjections.py::test_stop_preserves_queue
---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_stop_preserves_queue` |
| CI Job | `regression-ui` |

## Test Scenario

Verify queued messages are preserved (not discarded) when run is stopped.

## Automated Steps

1. Login and start long-running agent task
2. Queue 2 interjections
3. Click Stop button
4. Verify queued messages preserved in timeline
5. Verify message text matches original
6. Send new message to continue chatting

## Assertions

- Queued messages NOT deleted on stop
- Messages convert to normal user messages
- Text preserved exactly
- Chat continues normally
