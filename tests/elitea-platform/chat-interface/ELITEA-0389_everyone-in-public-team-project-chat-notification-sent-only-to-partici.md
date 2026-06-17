---
id: ELITEA-0389
title: "@Everyone in public team project chat: notification sent only to participants, not to view-only members"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2094, EliteaAI/elitea_issues#4167]
---
# ELITEA-0389: @Everyone in public team project chat: notification sent only to participants, not to view-only members

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a public/team-visible chat, `@Everyone` sends notifications only to users who are listed in the participants panel at the time of tagging — not to all members who can view the chat.

**Coverage:**
- `@Everyone` tag is correctly inserted and message is sent in a public team chat
- Participants listed in the panel at time of tagging receive a notification
- View-only members who have access to the public chat but are NOT in the participants panel do NOT receive a notification
- Notification scoping is based on participants panel membership, not chat visibility

## Preconditions

- Logged into ELITEA at {{base_url}}
- A team project exists with a public/team-visible chat
- User A and User B are listed in the participants panel (explicitly added or have written in the chat)
- User C is a team member who can view the public chat but has never been added to it and has never written in it — User C does NOT appear in the participants panel
- All three users have active sessions available for notification verification

## Test Data

| Role | User | In participants panel? | Can view chat? |
|---|---|---|---|
| Sender | User A | Yes | Yes |
| Participant | User B | Yes | Yes |
| Viewer only | User C | No | Yes (public visibility) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the public team project chat as User A | Chat loads; participants panel shows only User A and User B — User C is absent from the panel |
| 2 | Go to Participants → Users and click 'All users', or type `@Everyone` directly in the message input | `@Everyone` tag is inserted into the chat input |
| 3 | Send the message | Message is sent and rendered in the conversation history with `@Everyone`; participants panel remains unchanged |
| 4 | Log in as User B and open the Notification tab | User B has received a notification for the `@Everyone` mention (is an active participant) |
| 5 | Log in as User C and open the Notification tab | User C has NOT received any notification — they have view access only, not participant status |

## Expected Final State

User C has NOT received any notification — they have view access only, not participant status

## Pass/Fail Criteria

**Pass:**
- `@Everyone` is correctly inserted and message is sent
- User B (participant) receives the notification
- User C (viewer only, not in participants panel) does NOT receive any notification

**Fail:**
- User C receives a notification despite not being listed in the participants panel
- User B does not receive a notification despite being an active participant
- `@Everyone` is not inserted when triggered via "All users" (original bug from #2094)
