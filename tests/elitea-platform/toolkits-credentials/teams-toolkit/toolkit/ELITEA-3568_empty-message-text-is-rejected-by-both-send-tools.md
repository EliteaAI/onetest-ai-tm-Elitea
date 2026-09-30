---
id: ELITEA-3568
title: "Empty Message Text Is Rejected by Both Send Tools"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3568: Empty Message Text Is Rejected by Both Send Tools

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify `send_chat_message` and `send_channel_message` reject an empty/whitespace-only `message` with a clear validation error rather than sending a blank message or failing deep inside the Graph call.

## Preconditions

- Teams toolkit with `send_chat_message` and `send_channel_message` enabled, linked to an authorized credential
- A valid existing chat and a valid team/channel

## Test Data

| Variant | Tool | message | Expected |
|---|---|---|---|
| A | send_chat_message | `""` (empty string) | Rejected, nothing posted |
| B | send_chat_message | `"   "` (whitespace-only) | Rejected, nothing posted |
| C | send_channel_message | `""` (empty string) | Rejected, nothing posted |
| D | send_channel_message | `"   "` (whitespace-only) | Rejected, nothing posted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `send_chat_message` against a valid existing chat per Variants A and B | Both calls fail with a clear validation error; nothing is posted |
| 2 | Call `send_channel_message` against a valid team/channel per Variants C and D | Both calls fail with a clear validation error; nothing is posted |

## Expected Final State

No blank message exists in either the chat or the channel after the test.

## Pass/Fail Criteria

**Pass:**
- All four empty/whitespace variants are rejected with a clear validation error before any Graph call is made

**Fail:**
- Any variant sends a blank message, or fails with an unclear error deep inside the Graph call
