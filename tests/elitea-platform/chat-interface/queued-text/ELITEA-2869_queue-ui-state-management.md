---
id: ELITEA-2869
title: "Verify queue area displays correct count and status"
priority: high
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, ui, queue]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Feature enabled at platform and project level
- Agent/LLM run active

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Message 1 | "First queued message" |
| Message 2 | "Second queued message" |
| Message 3 | "Third queued message" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run | Run begins, composer enabled |
| 2 | Queue 1st message | Queue area appears showing "Waiting messages · 1" |
| 3 | Queue 2nd message | Count updates to "Waiting messages · 2" |
| 4 | Queue 3rd message | Count updates to "Waiting messages · 3" |
| 5 | Verify message order in queue | Messages in chronological order (first at top) |
| 6 | Verify status indicators | Each message shows "Queued" status |
| 7 | Wait for all messages to be processed | Queue area hides when empty |

## Expected Final State

- Queue area hidden after all messages processed
- All counts were accurate during queuing
- Messages displayed in correct order

## Pass/Fail Criteria

**Pass:**
- Count increments correctly with each message
- "Queued" status shown for each message
- Chronological order maintained
- Queue area hides when empty

**Fail:**
- Count incorrect or not updating
- Status indicators missing
- Wrong order in queue
- Queue area visible when empty
