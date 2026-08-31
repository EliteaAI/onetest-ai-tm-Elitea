---
id: ELITEA-2864
title: "Verify basic interjection queuing and sequential processing"
priority: critical
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, queue]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Feature enabled at platform and project level
- Active chat with agent/LLM capable of long-running responses

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interjection 1 | "make it short" |
| Interjection 2 | "make it easy" |
| Interjection 3 | "add examples" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send initial message that triggers long agent/LLM response | Agent/LLM starts processing, composer remains enabled |
| 2 | While agent/LLM is running, type "make it short" and click Send | Message appears in "Waiting messages" queue with "Queued" status |
| 3 | Type "make it easy" and click Send | Second message queued, count shows "Waiting messages · 2" |
| 4 | Type "add examples" and click Send | Third message queued, count shows "Waiting messages · 3" |
| 5 | Wait for initial response to complete | Initial response displayed in chat |
| 6 | Observe processing of queued messages | All 3 queued messages processed simultaneously |
| 7 | Verify response display | Three distinct responses displayed sequentially |

## Expected Final State

- All 3 interjections processed with individual responses
- UI shows "You interjected:" labels for each message
- Responses in correct chronological order
- Queue area empty/hidden

## Pass/Fail Criteria

**Pass:**
- All 3 messages queued successfully with "Queued" status
- Each queued message receives separate response
- Responses displayed sequentially in correct order
- "You interjected:" labels visible

**Fail:**
- Messages not queued or lost
- Messages combined into single response
- Responses out of order
- Queue count incorrect
