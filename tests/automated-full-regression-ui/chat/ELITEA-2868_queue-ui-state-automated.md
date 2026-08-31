---
id: ELITEA-2868
title: "Automated: Queue UI state management"
priority: high
type: automated
module: interjections
status: draft
execution_type: automated
tags: [feat:chat, r-2.0.6, interjection, ui, automated, regression]
requirements: [EliteaAI/elitea_issues#6115]
automation_test_id: test_queue_ui_state
code_ref: tests/automated-full-regression-ui/chat/test_interjections.py::test_queue_ui_state
---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_queue_ui_state` |
| CI Job | `regression-ui` |

## Test Scenario

Verify queue area displays correct count and status indicators.

## Automated Steps

1. Login and start agent run
2. Queue message 1, verify "Waiting messages · 1"
3. Queue message 2, verify "Waiting messages · 2"
4. Queue message 3, verify "Waiting messages · 3"
5. Verify "Queued" status on each message
6. Wait for all to process
7. Verify queue area hides when empty

## Assertions

- Count increments correctly
- Status indicators present
- Chronological order maintained
- Queue area hidden when empty
