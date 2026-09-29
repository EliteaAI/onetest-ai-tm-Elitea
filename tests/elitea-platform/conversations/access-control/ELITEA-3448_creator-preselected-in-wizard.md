---
id: ELITEA-3448
title: "Creator is Pre-Selected in Restrict Access Wizard"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, wizard, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3448: Creator is Pre-Selected in Restrict Access Wizard

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the conversation creator/author is automatically pre-selected in the Restrict Access wizard.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with multiple participants (at least 3 users)

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Conversation State | Public |
| Participants | At least 3 users |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Right-click on the public conversation | Action dropdown opens |
| 2 | Click "Restrict access" | Restrict Access wizard/modal opens |
| 3 | Verify wizard title | Title displays "Restrict access" |
| 4 | Verify conversation name shown | Conversation name displayed in wizard header |
| 5 | Locate "User participants" section | Section is visible with participant chips |
| 6 | Find creator/author in the list | Author is listed among participants |
| 7 | Verify author's selection state | Author chip is PRE-SELECTED (checked/highlighted) |
| 8 | Verify author is clearly identifiable | Author shows name/avatar and is distinguishable |

## Expected Final State

- Author is always present and pre-selected in wizard
- Author cannot be in unselected state initially
- Wizard clearly shows who the author is

## Teardown

- Click Cancel to close wizard without changes
