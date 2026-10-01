---
id: ELITEA-0397
title: "@Mention Notification Contains Sender Context and Navigates to Correct Chat"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4167, EliteaAI/elitea_issues#6368]
---
# ELITEA-0397: @Mention Notification Contains Sender Context and Navigates to Correct Chat

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the user mention notification contains sender identity and conversation context, and that clicking it navigates User B to the correct chat conversation.

**Coverage:**
- Notification text references the sender's name or username
- Notification references the conversation context
- Clicking the notification navigates to the correct Team Project chat conversation
- The message containing the user mention is visible after navigation

## Preconditions

- User A and User B are members of the same Team Project
- Both are participants in a named Team Project chat conversation

## Test Data

- Sender username: e.g., user_a_name (note before test)
- Conversation name: note before test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A. Note the name of the Team Project chat conversation. Add @User_B to the message by typing `+User_B` directly in the chat input or clicking User B in the PARTICIPANTS panel. Send the message (e.g., 'Please review this, @User_B.'). | Message is sent with the @User_B tag visible. Conversation name is noted. |
| 2 | Log out. Log in as User B. Navigate to the Notification tab. | Notification tab is open. |
| 3 | Locate the user mention notification. Read its content and verify it includes User A's name or username. | Notification text references User A as the sender (e.g., 'User_A mentioned you'). |
| 4 | Verify the notification references the chat or conversation context (e.g., conversation name or 'in chat'). | Notification contains a reference to the conversation where the user mention occurred. |
| 5 | Click the notification entry or its action link. | Browser navigates to the correct Team Project chat conversation where User B was mentioned. |
| 6 | Verify the message containing the @User_B tag is visible in the conversation thread. | The user mention message from User A is visible in the chat. |

## Expected Final State

The user mention message from User A is visible in the chat.

## Pass/Fail Criteria

**Pass:**
- Notification includes sender's name or username
- Notification references the conversation
- Clicking notification navigates to the correct chat conversation containing the user mention message

**Fail:**
- Notification content is blank or missing sender/conversation context
- Clicking notification navigates to the wrong page, produces an error, or does nothing
