---
id: ELITEA-3460
title: "Restrict Conversation to Author Only (Minimum Participants)"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, edge-case, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3460: Restrict Conversation to Author Only (Minimum Participants)

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a conversation can be restricted to only the author (minimum valid participant state).

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with 5+ participants and AI agents

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Initial Participants | 5+ users + AI agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | All participants displayed |
| 2 | Use "Remove all user participants" bulk action | Only author remains in users |
| 3 | Use "Remove all AI participants" bulk action | AI section is empty |
| 4 | Verify only author is selected | Single chip for author only |
| 5 | Click "Restrict access" button | Operation SUCCEEDS (valid minimum state) |
| 6 | Wizard closes | No error shown |
| 7 | Verify conversation accessible | Author can open conversation |
| 8 | View all messages | Full history visible |
| 9 | Send new message | Message sends successfully |
| 10 | Login as any previous participant | User CANNOT access |
| 11 | Search for conversation as other user | NOT found |
| 12 | As author, re-open wizard | Can add participants back |

## Expected Final State

- Conversation exists with only author access
- Author has full functionality
- Can re-add participants later

## Teardown

- None required
