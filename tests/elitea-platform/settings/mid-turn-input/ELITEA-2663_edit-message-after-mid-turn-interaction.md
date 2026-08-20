---
id: ELITEA-2663
title: "Verify Edit message functionality after mid-turn interaction"
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
- User has completed a turn with mid-turn interaction

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Complete a turn with mid-turn input | Turn completes normally |
| 2 | Locate the Edit button on the original user message | Edit button is visible |
| 3 | Click Edit and modify the message | Edit interface opens, message can be modified |
| 4 | Save the edit and regenerate | Edit is saved, regeneration triggered |
| 5 | Verify the regenerated response | New response reflects the edited message |

## Expected Final State

Edit and regenerate flow works correctly after mid-turn interactions.

## Pass/Fail Criteria

**Pass:**
- Edit button works
- Message can be modified
- Regeneration produces new response

**Fail:**
- Edit fails
- Regeneration errors out
- Conversation state corrupted
