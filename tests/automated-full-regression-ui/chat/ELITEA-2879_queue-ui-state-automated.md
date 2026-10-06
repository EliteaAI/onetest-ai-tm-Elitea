---
id: ELITEA-2879
title: "Automated: Queue UI state management"
priority: high
type: automated
module: interjections
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, ui, regression]
requirements: [EliteaAI/elitea_issues#6115]
---

# ELITEA-2879: Queue UI state management

**Module:** interjections · **Priority:** high · **Type:** automated

**Objective:** Verify queue area displays correct count and status indicators as messages are queued.

---

## Automation Details

| Field | Value |
|-------|-------|
| Framework | Playwright |
| Test File | `tests/automated-full-regression-ui/chat/test_interjections.py` |
| Test Function | `test_queue_ui_state` |
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
| 1 | Login and start agent run | Agent starts processing |
| 2 | Queue first message | Queue indicator appears showing "Waiting messages · 1" |
| 3 | Queue second message | Queue counter updates to "Waiting messages · 2" |
| 4 | Queue third message | Queue counter updates to "Waiting messages · 3" |
| 5 | Verify "Queued" status on each message | All three messages display "Queued" status badge |
| 6 | Verify chronological order in queue area | Messages appear in send order (1, 2, 3) |
| 7 | Wait for all messages to process | All messages receive responses sequentially |
| 8 | Verify queue area hides when empty | Queue indicator disappears when all messages processed |

---

## Expected Final State

Queue UI updates correctly with accurate counts, status indicators, and chronological order. Queue area hides when empty.

---

## Pass/Fail Criteria

**Pass:**
- Queue count increments correctly (1 → 2 → 3)
- "Queued" status indicators present on each message
- Chronological order maintained in queue display
- Queue area hidden when all messages processed

**Fail:**
- Queue count incorrect or not updating
- Status indicators missing or incorrect
- Messages displayed out of order
- Queue area remains visible when empty
