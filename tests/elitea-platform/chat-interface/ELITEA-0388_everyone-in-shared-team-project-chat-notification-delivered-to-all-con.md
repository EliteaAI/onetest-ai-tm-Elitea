---
id: ELITEA-0388
title: "@Everyone in shared team project chat: notification delivered to all conversation participants"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2094, EliteaAI/elitea_issues#4167, EliteaAI/elitea_issues#7489]
---
# ELITEA-0388: @Everyone in shared team project chat: notification delivered to all conversation participants

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that using `@Everyone` in a shared team project chat sends a notification to every user who is listed in the participants panel at the time of tagging.

**Coverage:**
- `@Everyone` tag is correctly inserted into the message input via "Everyone" in the users dropdown of the Users card
- Message is sent successfully with `@Everyone` rendered
- All active participants (explicitly added or having written in the chat) receive a notification in the Notification tab
- Notification is not missed for any participant

## Preconditions

- Logged into ELITEA at {{base_url}}
- A team project exists with a shared chat
- User A (the sender, owner) shared the chat with User B and User C via Share > Team (selected people); the Users card shows "3 users"
- User B and User C are logged into separate sessions for notification verification

## Test Data

| Role | User | In participants panel? |
|---|---|---|
| Sender | User A | Yes |
| Participant | User B | Yes |
| Participant | User C | Yes |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the shared team project chat as User A | Chat loads; Users card shows "3 users"; its dropdown lists User B and User C |
| 2 | Click the Users card count and then "Everyone", or type `@Everyone` directly in the message input | `@Everyone` tag is inserted into the chat input field |
| 3 | Type a message body (e.g., 'Please review this update') and click Send | Message is sent successfully; `@Everyone` is rendered in the conversation history |
| 4 | Log in as User B and open the Notification tab | User B has received a notification for the `@Everyone` mention in that chat |
| 5 | Log in as User C and open the Notification tab | User C has received a notification for the `@Everyone` mention in that chat |

## Expected Final State

User C has received a notification for the `@Everyone` mention in that chat

## Pass/Fail Criteria

**Pass:**
- `@Everyone` is correctly inserted into the input via "Everyone" or direct typing
- Message is sent and rendered correctly
- Both User B and User C receive the notification in their Notification tab

**Fail:**
- `@Everyone` is not inserted when "All users" is clicked (original bug scenario from EliteaAI/elitea_issues#2094)
- Any active participant (B or C) does not receive a notification
- Notification appears for a user not listed in the participants panel
