---
id: ELITEA-2866
title: "Automated: Attachment blocking during active run"
priority: critical
type: automated
module: interjections
status: draft
execution_type: automated
tags: [feat:chat, r-2.0.6, interjection, attachment, automated, regression]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6448]
automation_test_id: test_attachment_blocking
code_ref: tests/automated-full-regression-ui/chat/test_interjections.py::test_attachment_blocking
---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_attachment_blocking` |
| CI Job | `regression-ui` |

## Test Scenario

Verify attachments are blocked during active agent/LLM run.

## Automated Steps

1. Login and start agent run
2. Check attachment button state (should be disabled)
3. Attempt drag-and-drop file (should be blocked)
4. Send plain text interjection
5. Verify no attachment on queued message
6. Wait for run to complete
7. Verify attachment button re-enabled

## Assertions

- Attachment button disabled during run
- No files attached to interjections
- Attachment restored after run completes
