---
id: ELITEA-2660
title: "Verify mid-turn input handling when sent immediately after turn starts"
priority: high
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Analyze the pros and cons of remote work" |
| Quick mid-turn message | "From an employee perspective only" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the initial prompt | Agent turn starts |
| 2 | Immediately (within 1-2 seconds) send the mid-turn message | Message is sent |
| 3 | Observe system behavior | Message is either queued, delivered, or gracefully deferred |
| 4 | Wait for turn to complete | Turn completes without error |
| 5 | Review the outcome | Either mid-turn was processed OR it became a follow-up message |

## Expected Final State

Early mid-turn input is handled gracefully — either queued for delivery or deferred to become a new message. No silent drops or errors.

## Pass/Fail Criteria

**Pass:**
- Message is not silently dropped
- Either delivered mid-turn or falls back to new message
- No error messages
- Clear feedback on what happened

**Fail:**
- Message is silently dropped
- Error occurs
- System hangs or becomes unresponsive
