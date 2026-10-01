---
id: ELITEA-0391
title: "User mention autocomplete activates after adding a second participant to a team project chat"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4896, EliteaAI/elitea_issues#6368]
---
# ELITEA-0391: User mention autocomplete activates after adding a second participant to a team project chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the user mention autocomplete feature (triggered by `+`) activates dynamically once a second participant is added to a team project conversation — and does not appear before that point.

**Coverage:**
- No autocomplete when chat has only 1 participant (pre-condition validation)
- Participants panel updates after a new member is invited to the chat
- `+` trigger activates autocomplete dropdown after participant count reaches 2
- Mention selection and message sending function correctly in the newly activated state

## Preconditions

- Logged into ELITEA at {{base_url}}
- A team project is accessible
- A chat within that team project exists where only you are currently the participant (no other members added or wrote in this chat)
- Ability to add/invite another user (e.g., "Alice") to the conversation

## Test Data

| Data | Value |
|---|---|
| Initial participant count | 1 (only you) |
| Participant to add | "Alice" (a valid team member) |
| Expected participant count after addition | 2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the team project; open the chat where only you are participating | Chat view loads; participants panel shows 1 participant (you) |
| 2 | Click the input field and type `+` | No autocomplete dropdown appears (1 participant only) |
| 3 | Clear the input; add "Alice" to this conversation via the participants/invite control | Participants panel updates to show 2 participants: you and "Alice" |
| 4 | Click the input field and type `+` | User mention autocomplete dropdown appears and lists "Alice" |
| 5 | Click "Alice" in the dropdown | Dropdown closes; `@Alice` is inserted into the input |
| 6 | Send the message | Message with `@Alice` is submitted and visible in conversation history |

## Expected Final State

Message with `@Alice` is submitted and visible in conversation history

## Pass/Fail Criteria

**Pass:**
- No dropdown triggered with 1 participant (step 2)
- Dropdown correctly appears with "Alice" listed after she is added (step 4)
- Selection and send complete without errors

**Fail:**
- Dropdown appears before any second participant is added
- Dropdown does not appear even after "Alice" is added
- Any error or crash when transitioning from 1 to 2 participants
