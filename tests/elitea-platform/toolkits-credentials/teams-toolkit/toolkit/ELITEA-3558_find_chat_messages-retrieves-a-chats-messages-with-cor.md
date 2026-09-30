---
id: ELITEA-3558
title: "find_chat_messages — Retrieves a Chat's Messages With Correct New/Unread Semantics"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3558: find_chat_messages — Retrieves a Chat's Messages With Correct New/Unread Semantics

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `find_chat_messages` returns a chat's messages oldest-first, correctly determines which are "new," and that the returned watermark/`latest_message_id` can be used to continue from where the previous call left off.

## Preconditions

- Teams toolkit with `find_chat_messages` enabled, linked to an authorized credential
- A chat with existing message history, including some read and some unread messages, and messages from both the signed-in user and others

## Test Data

- N/A (sequential scenario, see Steps)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `find_chat_messages` for the chat with no `since`/`after_message_id` | `new_means` reports "unread"; only messages created after the user's last-read time are flagged `is_new` |
| 2 | Call `find_chat_messages` again passing the previous result's `watermark` as `since` | Only messages created after that watermark are returned |
| 3 | Send a new message to the chat, then call `find_chat_messages` passing the prior `latest_message_id` as `after_message_id` | The new message is returned; the anchor message itself is excluded |
| 4 | Call `find_chat_messages` with `include_own` omitted, then with `include_own=true` | Messages sent by the signed-in user are excluded by default and included when `include_own=true` |

## Expected Final State

Watermark-based and ID-based continuation both correctly scope results without gaps or duplicate anchors.

## Pass/Fail Criteria

**Pass:**
- "New" semantics, watermark continuation, and `include_own` all behave exactly as documented

**Fail:**
- Any of the above misclassifies messages, includes the anchor message, or fails to advance correctly
