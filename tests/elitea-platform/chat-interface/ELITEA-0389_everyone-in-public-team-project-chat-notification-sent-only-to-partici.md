---
id: ELITEA-0389
title: "@Everyone in a Whole team chat: notification sent to everyone with access"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2094, EliteaAI/elitea_issues#4167, EliteaAI/elitea_issues#7489, EliteaAI/elitea_issues#7523]
---
# ELITEA-0389: @Everyone in a Whole team chat: notification sent to everyone with access

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a chat shared with Whole team, `@Everyone` sends a notification to every project member who has access to the chat, including members who have never opened it.

**Coverage:**
- `@Everyone` tag is correctly inserted and message is sent in a Whole team chat
- Existing participants receive a notification
- Members with access through Whole team who have never opened the chat also receive a notification
- Notification scoping is based on chat access, not on participant records

## Preconditions

- Logged into ELITEA at {{base_url}}
- A team project exists with a chat shared with Whole team (Share > Team)
- User A (owner) and User B have written in the chat
- User C is a team member who has access through Whole team but has never opened the chat
- All three users have active sessions available for notification verification

## Test Data

| Role | User | In participants panel? | Can view chat? |
|---|---|---|---|
| Sender | User A | Yes | Yes |
| Participant | User B | Yes | Yes |
| Whole team member, never opened | User C | No | Yes (Whole team) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Whole team chat as User A | Chat loads; Users card shows "Whole Team (N)"; its dropdown lists User C |
| 2 | Click the Users card count and then "Everyone", or type `@Everyone` directly in the message input | `@Everyone` tag is inserted into the chat input |
| 3 | Send the message | Message is sent and rendered in the conversation history with `@Everyone` |
| 4 | Log in as User B and open the Notification tab | User B has received a notification for the `@Everyone` mention |
| 5 | Log in as User C and open the Notification tab | User C has received a notification for the `@Everyone` mention (has access through Whole team) |

## Expected Final State

User B and User C have received a notification for the `@Everyone` mention

## Pass/Fail Criteria

**Pass:**
- `@Everyone` is correctly inserted and message is sent
- User B (participant) receives the notification
- User C (Whole team access, never opened the chat) receives the notification

**Fail:**
- User C does not receive a notification despite having access through Whole team
- User B does not receive a notification
- `@Everyone` is not inserted when triggered via "Everyone" (original bug from EliteaAI/elitea_issues#2094)
