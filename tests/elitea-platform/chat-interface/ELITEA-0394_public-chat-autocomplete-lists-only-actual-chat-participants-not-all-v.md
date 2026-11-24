---
id: ELITEA-0394
title: "Whole team chat: user autocomplete lists everyone with access except the current user"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4896, EliteaAI/elitea_issues#6368, EliteaAI/elitea_issues#7489, EliteaAI/elitea_issues#7718]
---
# ELITEA-0394: Whole team chat: user autocomplete lists everyone with access except the current user

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a chat shared with Whole team, the user mention autocomplete suggests every project member with access (except the current user), including members who have never opened the chat, and that mentioning such a member works.

**Coverage:**
- Autocomplete in a Whole team chat lists all teammates with access, except the current user
- Members who have never opened the chat are listed and can be mentioned
- Partial-name filtering works across all teammates
- Mentioning a member who has never opened the chat adds them as a participant and notifies them

## Preconditions

- Logged into ELITEA at {{base_url}}
- A chat in a team project is shared with Whole team (5+ members)
- "Alice" and "Bob" have written in the chat
- A third team member "Carol" has access through Whole team but has never opened the chat
- Logged in as the owner of the chat

## Test Data

| Role | User | Active in chat? |
|---|---|---|
| Active participant (added) | "Alice" | Yes |
| Active participant (wrote) | "Bob" | Yes |
| Whole team member, never opened the chat | "Carol" | No |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Whole team chat | Chat view loads; Users card shows "Whole Team (N)" |
| 2 | Click the message input and type `+` | Autocomplete dropdown appears |
| 3 | Inspect the dropdown entries | All teammates except the current user are listed, including "Carol" |
| 4 | Type `C` after `+` (filtering for "Carol") | "Carol" is suggested |
| 5 | Clear `C`; type `Al` to filter for Alice | Dropdown narrows to "Alice" only |
| 6 | Select "Carol"; complete and send the message | `@Carol` is inserted; message is sent; Carol becomes a participant and is notified |

## Expected Final State

`@Carol` is inserted and sent; Carol is notified and listed as a participant

## Pass/Fail Criteria

**Pass:**
- Dropdown lists all teammates with access except the current user, including Carol
- Filtering works across all teammates
- Mentioning Carol sends the message and notifies her

**Fail:**
- Only existing participants are listed; Carol is missing
- The current user is listed
- Mentioning Carol fails or she is not notified
