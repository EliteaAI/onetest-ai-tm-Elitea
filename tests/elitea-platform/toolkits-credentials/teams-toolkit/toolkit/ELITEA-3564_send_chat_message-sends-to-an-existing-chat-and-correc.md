---
id: ELITEA-3564
title: "send_chat_message — Sends to an Existing Chat and Correctly Creates 1:1/Group Chats When Needed"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3564: send_chat_message — Sends to an Existing Chat and Correctly Creates 1:1/Group Chats When Needed

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `send_chat_message` can send to an existing chat and can create new 1:1/group chats on demand without duplicating existing ones.

## Preconditions

- Teams toolkit with `send_chat_message` enabled, linked to an authorized credential
- A second test user in the same tenant, with no pre-existing 1:1 or group chat with the signed-in user (or ability to reset that state)

## Test Data

| Variant | Target | Expected |
|---|---|---|
| A | existing chat ID | Message posted to that chat |
| B | `recipients` = single email, no existing 1:1 chat | New 1:1 chat created and message delivered |
| C | `recipients` = same single email again | Existing 1:1 chat reused, not duplicated |
| D | `recipients` = multiple emails, no existing group chat, with `topic` | New group chat created with that topic and all recipients |
| E | same recipient set as D, sent again | Existing group chat reused, not duplicated |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a message per Variant A | Message is posted; `message_id`/`chat_id` are returned |
| 2 | Send a message per Variant B | New 1:1 chat is created (`chat_created: true` where applicable) and the message is delivered |
| 3 | Send a message per Variant C | The existing 1:1 chat is reused, not duplicated |
| 4 | Send a message per Variant D | New group chat is created with the given topic and all recipients |
| 5 | Send a message per Variant E | The existing group chat is reused rather than a new one being created |

## Expected Final State

Exactly one 1:1 chat and one group chat exist for the tested recipient sets, each containing all sent messages.

## Pass/Fail Criteria

**Pass:**
- Existing-chat sends work; new-chat creation and chat reuse both behave exactly as documented with no duplicates

**Fail:**
- A duplicate 1:1 or group chat is created on a repeat send, or an existing chat is not reused
