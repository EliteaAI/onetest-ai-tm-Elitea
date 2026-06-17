---
id: ELITEA-0541
title: "Save and apply — older conversation history is not modified"
priority: critical
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0541: Save and apply — older conversation history is not modified

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after Save and apply, only the last user-assistant pair is affected and all older messages remain unchanged.

**Coverage:**
- Older user messages unchanged
- Older assistant messages unchanged
- Message count is consistent (no duplication or removal)

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with 3+ user-assistant exchanges

## Test Data

- Conversation with messages: Msg1 → Resp1, Msg2 → Resp2, Msg3 → Resp3
- Edit Msg3 to something different

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation with 3 exchanges. Note the content of messages 1 and 2 (both user and assistant). | Contents of Msg1, Resp1, Msg2, Resp2 are noted. |
| 2 | Click Edit on the last user message (Msg3). Modify the text and click "Save and apply". | Regeneration begins for the last response. |
| 3 | After the new response completes, verify Msg1 and Resp1. | Both are unchanged — exact same content as noted in step 1. |
| 4 | Verify Msg2 and Resp2. | Both are unchanged — exact same content as noted in step 1. |
| 5 | Count total messages in the conversation. | Total message count is the same as before (no duplicate messages added, no messages removed). Only Resp3 was replaced. |

## Expected Final State

Total message count is the same as before (no duplicate messages added, no messages removed). Only Resp3 was replaced.

## Pass/Fail Criteria

**Pass:**
- All messages prior to the last exchange are unchanged
- No messages duplicated or removed
- Only the last assistant response was regenerated

**Fail:**
- Older messages are modified or removed
- Duplicate messages appear
- Entire conversation is regenerated
