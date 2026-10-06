---
id: ELITEA-2877
title: "Automated: Attachment blocking during active run"
priority: critical
type: automated
module: interjections
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, attachment, regression]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6448]
---

# ELITEA-2877: Attachment blocking during active run

**Module:** interjections · **Priority:** critical · **Type:** automated

**Objective:** Verify attachments are blocked during active agent/LLM run.

---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_attachment_blocking` |
| CI Job | `regression-ui` |

---

## Preconditions

- User is logged in to the Elitea platform.
- Chat interface is accessible.
- Test file available for drag-and-drop testing.

---

## Test Data

| Field | Value |
|-------|-------|
| Test file | Any small file (e.g., test.txt) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login and start agent run | Agent starts processing message |
| 2 | Check attachment button state | Attachment button is disabled (grayed out) |
| 3 | Attempt to drag and drop a file onto chat input | File drop is blocked, no file attached |
| 4 | Send plain text interjection message | Message is queued successfully |
| 5 | Verify no attachment on queued message | Queued message has no attachment indicator |
| 6 | Wait for agent run to complete | Agent response finishes |
| 7 | Verify attachment button re-enabled | Attachment button becomes active/clickable again |

---

## Expected Final State

Attachments blocked during agent run, plain text interjections allowed, attachment button re-enabled after completion.

---

## Pass/Fail Criteria

**Pass:**
- Attachment button disabled during agent run
- Drag-and-drop file upload blocked
- Plain text interjection queued successfully without attachment
- Attachment button re-enabled after run completes

**Fail:**
- Attachment button remains enabled during run
- File attachment succeeds during active run
- Attachment button not restored after completion
