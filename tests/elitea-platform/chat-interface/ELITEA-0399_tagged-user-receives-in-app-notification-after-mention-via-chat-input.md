---
id: ELITEA-0399
title: "Tagged User Receives In-App Notification After @Mention via Chat Input [Parametrized by Role]"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat]
requirements: [EliteaAI/elitea_issues#4167]
---
# ELITEA-0399: Tagged User Receives In-App Notification After @Mention via Chat Input [Parametrized by Role]

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a user sends a chat message tagging another user via the @ trigger in the chat input field, the mentioned user receives a notification in the Notification tab — regardless of role combination.

**Coverage:**
- @mention via typed @ in Team Project chat input generates notification for mentioned user
- Sender (User A) does NOT receive a self-notification
- Notification is delivered across all role combinations: Admin→Editor, Admin→Viewer, Editor→Admin, Editor→Viewer, Viewer→Admin, Viewer→Editor

## Preconditions

- Two user accounts (User A and User B) are members of the same Team Project
- Both users are already added as participants in a shared Team Project chat conversation
- Logged in as User A (sender)

## Test Data

Role combinations to test:
| User A (Sender) | User B (Recipient) |
|---|---|
| Admin | Editor |
| Admin | Viewer |
| Editor | Admin |
| Editor | Viewer |
| Viewer | Admin |
| Viewer | Editor |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A. Open the Team Project chat conversation that includes User B as a participant. | Chat is open. User B is visible in the PARTICIPANTS panel. |
| 2 | To mention User B, use one of these methods: (a) type @User_B directly in the chat input field, OR (b) click on User B's name/avatar in the PARTICIPANTS panel to insert the mention tag into the input. Complete the message (e.g., 'Hey @User_B, please check this.') and send. | Message is sent. The @User_B tag appears in the chat thread. |
| 3 | Open User A's Notification tab (bell icon or sidebar navigation). | User A's Notification tab contains no notification related to sending this @mention. |
| 4 | Log out as User A. Log in as User B. Navigate to the Notification tab. | User B's Notification tab is open. |
| 5 | Check for a notification indicating User B was mentioned in the chat. | Exactly one notification entry is present indicating User B was mentioned by User A. |
| 6 | Repeat Steps 1–5 for all six role combinations listed in Test Data. | In every role combination, User B receives exactly one notification. User A never receives a self-notification. |

## Expected Final State

In every role combination, User B receives exactly one notification. User A never receives a self-notification.

## Pass/Fail Criteria

**Pass:**
- For every role combination, User B sees a notification in the Notification tab after being @mentioned
- User A does NOT receive any notification for their own @mention

**Fail:**
- User B does not receive a notification for one or more role combinations
- User A incorrectly receives a notification for their own @mention action
