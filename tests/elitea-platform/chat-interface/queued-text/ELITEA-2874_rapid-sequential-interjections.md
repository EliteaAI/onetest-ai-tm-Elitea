---
id: ELITEA-2874
title: "Verify rapid message queuing without race conditions"
priority: medium
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, performance, race-condition]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agent/LLM run active with sufficient processing time

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Message 1 | "Rapid test 1" |
| Message 2 | "Rapid test 2" |
| Message 3 | "Rapid test 3" |
| Message 4 | "Rapid test 4" |
| Message 5 | "Rapid test 5" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run with long task | Run begins |
| 2 | Quickly type and send 5 messages in 2-3 seconds | All messages accepted |
| 3 | Verify all messages in queue | Count shows "Waiting messages · 5" |
| 4 | Verify message order | Messages in chronological order |
| 5 | Wait for all messages to be processed | All 5 responses generated |
| 6 | Verify response count | Exactly 5 responses, no duplicates |
| 7 | Observe UI during rapid entry | No flickering, freezing, or errors |

## Expected Final State

- All 5 messages processed with individual responses
- Correct order preserved
- No race condition artifacts

## Pass/Fail Criteria

**Pass:**
- All 5 messages queued successfully
- Correct chronological order
- No messages lost or duplicated
- UI remains stable

**Fail:**
- Messages lost during rapid entry
- Duplicate messages created
- Out-of-order processing
- UI freezes or errors
