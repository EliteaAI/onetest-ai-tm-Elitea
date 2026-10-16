---
id: ELITEA-2629
title: "Team Project Duplicate - No Unintended Participant Crossover"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, participant-isolation, team-project, P1]
requirements: [3837]
---
# ELITEA-2629: Team Project Duplicate - No Unintended Participant Crossover

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicating a chat in a team project does not gain unintended AI participants or users beyond those in the original chat.

## Preconditions

- User is logged in to {{base_url}}
- Team project with multiple users available
- Team project has multiple AI participants available
- Original chat has specific subset of participants

## Test Data

- URL: {{base_url}}
- Team project
- Original chat: User A, User B, Agent X
- Available but NOT in chat: User C, Agent Y, Pipeline Z

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify team project has additional users not in the chat | User C exists in project, not in chat |
| 2 | Verify team project has additional AI resources not in chat | Agent Y, Pipeline Z available but not added |
| 3 | Open original chat and document exact participants | User A, User B, Agent X only |
| 4 | Duplicate the chat | Duplicate created |
| 5 | Open duplicated chat participants panel | Participants panel displays |
| 6 | Verify only User A and User B present | No User C added |
| 7 | Verify only Agent X present in AI section | No Agent Y or Pipeline Z added |
| 8 | Count total participants in duplicate | Should match original count exactly |
| 9 | Verify no configuration inheritance from project defaults | Only explicit participants copied |

## Expected Final State

- Duplicate contains only original participants
- No additional users from team added
- No additional AI from project resources added
- Exact participant match with original
- No crossover or contamination

## Pass/Fail Criteria

**Pass:**
- Exact participant match with original
- No User C added to duplicate
- No Agent Y or Pipeline Z added
- Participant count identical
- No unintended crossover

**Fail:**
- Additional users added from team
- Additional AI participants added from project
- Participant count higher than original
- Configuration inherits unintended resources
