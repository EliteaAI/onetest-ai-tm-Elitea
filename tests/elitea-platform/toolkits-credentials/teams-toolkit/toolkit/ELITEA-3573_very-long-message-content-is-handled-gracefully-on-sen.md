---
id: ELITEA-3573
title: "Very Long Message Content Is Handled Gracefully on Send"
priority: medium
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3573: Very Long Message Content Is Handled Gracefully on Send

**Module:** Teams Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `send_chat_message` and `send_channel_message` handle a message body near or beyond Microsoft Teams' size limits with a clear error rather than an obscure failure or a corrupted partial post.

## Preconditions

- Teams toolkit with `send_chat_message` and `send_channel_message` enabled, linked to an authorized credential
- A valid existing chat and a valid team/channel
- A prepared very long text string (e.g. approaching or exceeding Teams' known message size limit)

## Test Data

| Variant | Tool | message length | Expected |
|---|---|---|---|
| A | send_chat_message | very long (near limit) | Either sends successfully in full, or fails with a clear size-limit error |
| B | send_channel_message | exceeds known limit | Fails with a clear size-limit error; no partial/corrupted message posted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a chat message per Variant A | Message either sends in full and displays intact in Teams, or fails with a clear size-limit error |
| 2 | Send a channel message per Variant B | Call fails with a clear size-limit error; no partial or corrupted message appears in the channel |

## Expected Final State

No corrupted or partially-posted message exists in either the chat or the channel.

## Pass/Fail Criteria

**Pass:**
- Oversized content either sends completely intact or is rejected with a clear size-limit error, with no partial posts

**Fail:**
- A partial/corrupted message is posted, or the call fails with an unclear/generic error
