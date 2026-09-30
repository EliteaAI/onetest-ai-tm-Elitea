---
id: ELITEA-3464
title: "Restrict Access Dialog Wording is Clear and Unambiguous"
priority: medium
type: regression
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, ui, ux, bug-verification, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283, EliteaAI/elitea_issues#6798]
---
# ELITEA-3464: Restrict Access Dialog Wording is Clear and Unambiguous

**Module:** Conversations · **Priority:** Medium · **Type:** Regression / Bug Verification

**Objective:** Verify that the Restrict Access dialog text clearly explains the outcome of the action (Bug #6798 verification).

**Bug Reference:** [#6798](https://github.com/EliteaAI/elitea_issues/issues/6798) - Restrict Access Dialog Contains Ambiguous Wording

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A conversation exists with multiple participants

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Bug | #6798 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a conversation with multiple participants | Conversation opens |
| 2 | Open the "Restrict Access" wizard | Wizard/dialog opens |
| 3 | Read the description/confirmation text | Text is displayed |
| 4 | Evaluate if text clearly explains: Who currently has access | Clear identification |
| 5 | Evaluate if text clearly explains: Who will have access after confirmation | Clear distinction |
| 6 | Evaluate if wording uses consistent terminology | No confusion between "selected" and "existing selected" |

## Expected Final State

- Dialog text clearly and unambiguously states the outcome
- User can easily determine who will retain/lose access

## Pass/Fail Criteria

**Pass:**
- Text is clear, such as: "Only selected participants will have access to this conversation"
- No ambiguous overlapping concepts

**Fail (Bug #6798):**
- Text uses confusing wording like: "Restrict access to selected participants? Project members who are not selected will no longer be able to open this conversation. Existing selected participants will retain access."
- Users cannot easily distinguish between "selected" and "existing selected"

## Current Text (Ambiguous):
> "Restrict access to selected participants? Project members who are not selected will no longer be able to open this conversation. Existing selected participants will retain access."

## Expected Text (Clear):
> "Only selected participants will have access to this conversation."
> or
> "Unselected project members will no longer be able to open it."

## Teardown

- Click Cancel to close wizard
