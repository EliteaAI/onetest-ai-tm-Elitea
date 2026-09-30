---
id: ELITEA-3458
title: "Cancel Button Closes Wizard Without Changes"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, wizard, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3458: Cancel Button Closes Wizard Without Changes

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the Cancel button in the Restrict Access wizard closes the wizard without applying any changes.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with 5 participants
- Restrict Access wizard is open

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Participants | 5 users + AI agents |
| Conversation State | Public |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | Wizard displays with all 5 participants |
| 2 | Remove 2 user participants (click x) | 2 users removed from selection |
| 3 | Remove 1 AI participant | AI removed from selection |
| 4 | Verify changes in wizard | Only 3 users and fewer AI visible |
| 5 | Click "Cancel" button | Wizard closes |
| 6 | Verify no loading/processing shown | Immediate close, no API call |
| 7 | Right-click conversation, click "Restrict access" | Wizard opens again |
| 8 | Verify participant list | All 5 original participants are STILL selected |
| 9 | Login as one of the "removed" users | User CAN still access conversation |
| 10 | Verify conversation state | Still PUBLIC (unchanged) |

## Expected Final State

- No changes applied to conversation
- All participants retain access
- Conversation state unchanged

## Teardown

- None required
