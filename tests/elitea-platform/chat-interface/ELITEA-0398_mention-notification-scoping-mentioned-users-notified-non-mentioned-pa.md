---
id: ELITEA-0398
title: "@Mention Notification Scoping — Mentioned Users Notified, Non-Mentioned Participant Is Not"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat]
requirements: [EliteaAI/elitea_issues#4167]
---
# ELITEA-0398: @Mention Notification Scoping — Mentioned Users Notified, Non-Mentioned Participant Is Not

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that @mention notifications are scoped exclusively to the mentioned users — when multiple users are mentioned in one message they each receive a notification, while a non-mentioned participant in the same conversation receives nothing.

**Coverage:**
- Multiple @mentions in a single message each generate an individual notification
- Each mentioned user receives their own notification independently
- A conversation participant who was NOT mentioned receives no notification from the same message

## Preconditions

- Four user accounts (User A, B, C, D) are members of the same Team Project
- All four are added as participants in the same Team Project chat conversation

## Test Data

- Sender: User A
- Mentioned in one message: User B and User C
- Non-mentioned participant: User D
- Message: "Hey @User_B and @User_C, please review this."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A. Open the Team Project chat with Users B, C, and D present as participants. | Chat is open. Users B, C, and D are all visible in the PARTICIPANTS panel. |
| 2 | In the chat input, add @User_B by typing @User_B directly or clicking User B in the PARTICIPANTS panel. Then add @User_C in the same message using the same method. Do NOT tag User D. Send the message (e.g., 'Hey @User_B and @User_C, please review this.'). | Message is sent. Both @User_B and @User_C tags are present in the sent message. User D is not tagged. |
| 3 | Log out. Log in as User D (non-mentioned participant). Navigate to the Notification tab. | User D's Notification tab is open. |
| 4 | Verify no @mention notification exists from the message sent in Step 2. | User D has no notification from User A's @mention message. |
| 5 | Log out. Log in as User B. Navigate to the Notification tab. | User B's Notification tab is open. |
| 6 | Verify a notification is present for the @mention by User A. | User B has exactly one notification indicating they were mentioned. |
| 7 | Log out. Log in as User C. Navigate to the Notification tab. | User C's Notification tab is open. |
| 8 | Verify a notification is present for the @mention by User A. | User C has exactly one notification indicating they were mentioned. |

## Expected Final State

User C has exactly one notification indicating they were mentioned.

## Pass/Fail Criteria

**Pass:**
- User B has a notification in the Notification tab
- User C has a notification in the Notification tab
- User D (non-mentioned participant) has NO notification for this event

**Fail:**
- User B or User C does not receive a notification
- User D (non-mentioned) receives a notification
