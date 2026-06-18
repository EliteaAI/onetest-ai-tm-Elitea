---
id: ELITEA-0403
title: "`/` Autosuggest Filters Results in Real-Time Based on Typed Characters"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0403: `/` Autosuggest Filters Results in Real-Time Based on Typed Characters

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the autosuggest dropdown updates its listed items in real-time as the user types characters after `/`.

**Coverage:**
- Incremental typing narrows the list
- Deleting characters expands the list back
- Full name restores exact match

## Preconditions

- Artifacts and Jira Integration both added to Participants

## Test Data

- / shows both
- /J shows only Jira Integration
- /A shows only Artifacts

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat conversation with both toolkits in Participants. Type /. | Both Artifacts and Jira Integration appear in dropdown. |
| 2 | Type J (input is now /J). | Dropdown updates to show only Jira Integration. |
| 3 | Delete J, type A (input is now /A). | Dropdown updates to show only Artifacts. |
| 4 | Delete A (input is back to /). | Both toolkits reappear in dropdown. |

## Expected Final State

Both toolkits reappear in dropdown.

## Pass/Fail Criteria

**Pass:**
- Dropdown updates in real-time with each keystroke

**Fail:**
- Dropdown does not filter or requires Enter to update
