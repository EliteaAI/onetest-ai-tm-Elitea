---
id: ELITEA-2878
title: "Automated: Stop preserves queued messages"
priority: critical
type: automated
module: interjections
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, stop, regression]
requirements: [EliteaAI/elitea_issues#6115]
---

# ELITEA-2878: Stop preserves queued messages

**Module:** interjections · **Priority:** critical · **Type:** automated

**Objective:** Verify queued messages are preserved (not discarded) when agent run is stopped.

---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_stop_preserves_queue` |
| CI Job | `regression-ui` |

---

## Preconditions

- User is logged in to the Elitea platform.
- Chat interface is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Interjection 1 | "First queued message" |
| Interjection 2 | "Second queued message" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login and start long-running agent task | Agent starts processing |
| 2 | Queue first interjection message | First message appears in queue |
| 3 | Queue second interjection message | Second message appears in queue with count "Waiting messages · 2" |
| 4 | Click Stop button | Agent run stops immediately |
| 5 | Verify queued messages preserved in timeline | Both queued messages remain visible in chat timeline |
| 6 | Verify message text matches original | Message content is exactly preserved |
| 7 | Send new message to continue chatting | New message sent successfully and receives response |

---

## Expected Final State

Queued messages preserved as normal user messages in timeline, chat continues functioning normally.

---

## Pass/Fail Criteria

**Pass:**
- Queued messages NOT deleted when Stop clicked
- Messages convert to normal user messages in timeline
- Text preserved exactly as sent
- Chat continues normally after Stop

**Fail:**
- Queued messages deleted/lost on Stop
- Message text corrupted or changed
- Chat becomes unresponsive after Stop
