---
id: ELITEA-2658
title: "Verify Stop button functionality with mid-turn input enabled"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Write a comprehensive guide to machine learning algorithms" |
| Mid-turn message | "Include more examples" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message to trigger a long-running agent response | Agent starts processing, Stop button appears |
| 2 | Send a mid-turn message while agent is running | Mid-turn message is sent |
| 3 | Click the Stop button | Agent generation stops |
| 4 | Verify partial response is preserved | Partial work generated before stop is visible |
| 5 | Verify mid-turn message is handled | Mid-turn message is visible in history or gracefully handled |
| 6 | Verify ability to send new messages | Input field is enabled, new messages can be sent |

## Expected Final State

Stop button works correctly even when mid-turn input is in use. Partial work is preserved and the conversation can continue.

## Pass/Fail Criteria

**Pass:**
- Stop button stops agent execution
- Partial work is preserved
- Mid-turn message is handled gracefully
- New messages can be sent after stopping

**Fail:**
- Stop button doesn't work
- Work is lost
- Error occurs with pending mid-turn message
