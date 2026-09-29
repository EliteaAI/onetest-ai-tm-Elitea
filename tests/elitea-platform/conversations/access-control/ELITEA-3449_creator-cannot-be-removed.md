---
id: ELITEA-3449
title: "Creator Cannot Be Removed from Participants"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, permission, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3449: Creator Cannot Be Removed from Participants

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the conversation creator/author cannot be deselected or removed from the participant list in the Restrict Access wizard.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- Restrict Access wizard is open for a public conversation with multiple participants

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Wizard State | Open |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | Wizard displays with participants |
| 2 | Locate author chip in "User participants" section | Author is displayed and pre-selected |
| 3 | Examine author chip for (x) remove button | Either: (x) button is HIDDEN, DISABLED, or NOT PRESENT on author chip |
| 4 | If (x) is visible, attempt to click it | Action is PREVENTED |
| 5 | Verify validation message (if applicable) | Message indicates author cannot be removed |
| 6 | Verify author remains selected | Author chip still present and selected |
| 7 | Try using "Remove all user participants" bulk action | Author REMAINS selected even after bulk remove |
| 8 | Click "Restrict access" to confirm | Operation succeeds with author retained |

## Expected Final State

- Author always has access to conversation
- No way to create authorless conversation via UI
- Bulk remove actions preserve author

## Teardown

- None required
