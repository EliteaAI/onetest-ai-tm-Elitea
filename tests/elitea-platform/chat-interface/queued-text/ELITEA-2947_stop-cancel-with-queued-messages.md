---
id: ELITEA-2947
title: "Verify queued messages preserved when run is stopped"
priority: critical
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, stop, cancel]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Feature enabled at platform and project level
- Agent/LLM capable of long-running task

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interjection 1 | "Change the approach" |
| Interjection 2 | "Focus on key points" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send message to start long-running agent/LLM task | Agent/LLM begins processing |
| 2 | Queue first interjection while running | Message appears in "Waiting messages · 1" |
| 3 | Queue second interjection | Count shows "Waiting messages · 2" |
| 4 | Click Stop button before interjections are processed | Run stops, partial response may be shown |
| 5 | Observe behavior of queued messages | Messages preserved, not discarded |
| 6 | Verify messages in timeline | Messages convert to normal user messages |
| 7 | Send new message to continue chatting | Chat continues normally |

## Expected Final State

- Queued messages preserved in timeline as normal messages
- Message text exactly as originally typed
- User can continue chatting
- No error messages

## Pass/Fail Criteria

**Pass:**
- Queued messages NOT discarded on stop
- Messages convert to normal user messages
- Text preserved exactly
- Chat continues normally

**Fail:**
- Queued messages lost/deleted
- Messages corrupted or truncated
- Error messages shown
- Cannot continue chatting
