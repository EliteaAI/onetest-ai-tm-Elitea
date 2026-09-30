---
id: ELITEA-3570
title: "Sending to or Mentioning an Unknown/Invalid User Fails Clearly"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3570: Sending to or Mentioning an Unknown/Invalid User Fails Clearly

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that referencing a recipient or mention target that does not exist in the tenant (invalid email/user ID) produces an actionable error rather than a silent failure or a message sent without the mention resolving.

## Preconditions

- Teams toolkit with `send_chat_message` and `send_channel_message` enabled, linked to an authorized credential
- An email address confirmed not to correspond to any user in the tenant

## Test Data

| Variant | Tool | Field | Value | Expected |
|---|---|---|---|---|
| A | send_chat_message | recipients | unknown email | Fails with "user not found" style error; no chat created |
| B | send_chat_message / send_channel_message | mentions | unknown email | Fails clearly; message is not posted with a broken/unresolved mention |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `send_chat_message` with `recipients` set to Variant A's unknown email | Call fails with a clear "user not found" style error; no chat is created |
| 2 | Send a chat or channel message with `mentions` set to Variant B's unknown email | Call fails clearly rather than posting the message with a broken or unresolved mention |

## Expected Final State

No chat, message, or partially-resolved mention exists as a result of either call.

## Pass/Fail Criteria

**Pass:**
- Both calls fail with a clear, specific error and no partial side effects occur

**Fail:**
- Either call silently succeeds, creates a chat/message, or posts a message with a broken/unresolved mention
