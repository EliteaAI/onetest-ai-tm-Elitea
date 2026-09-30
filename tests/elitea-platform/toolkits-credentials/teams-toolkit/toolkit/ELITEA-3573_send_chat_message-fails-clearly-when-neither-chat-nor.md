---
id: ELITEA-3573
title: "send_chat_message Fails Clearly When Neither chat Nor recipients Is Provided"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3573: send_chat_message Fails Clearly When Neither chat Nor recipients Is Provided

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify `send_chat_message` cannot be called without specifying a target, and does not silently no-op or send to an unintended chat.

## Preconditions

- Teams toolkit with `send_chat_message` enabled, linked to an authorized credential

## Test Data

| Field | Value |
|-------|-------|
| message | valid text |
| chat | omitted |
| recipients | omitted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `send_chat_message` with a valid `message` but both `chat` and `recipients` omitted | Call fails with an explicit error stating one of `chat`/`recipients` is required |
| 2 | Confirm no message was sent | No chat is created and no message is posted anywhere |

## Expected Final State

No new chat or message exists as a result of the call.

## Pass/Fail Criteria

**Pass:**
- The call fails with an explicit, specific error and no message is sent

**Fail:**
- The call silently no-ops, sends to an unintended/default chat, or fails with a vague error
