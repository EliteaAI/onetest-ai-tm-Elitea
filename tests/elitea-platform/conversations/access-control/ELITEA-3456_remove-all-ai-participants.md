---
id: ELITEA-3456
title: "Remove All AI Participants Bulk Action"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, ai-participants, bulk-action, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3456: Remove All AI Participants Bulk Action

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Remove all AI participants" bulk action successfully removes all AI agents from the conversation.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A conversation exists with 3+ AI participants added
- Restrict Access wizard is open

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| AI Participants | 3+ AI agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | Wizard displays |
| 2 | Locate "AI participants" section | Section visible with AI agent chips |
| 3 | Count AI participant chips | 3+ AI agents displayed |
| 4 | Note the AI agent names | Names recorded for verification |
| 5 | Locate "Remove all AI participants" action | Button/link is visible |
| 6 | Click "Remove all AI participants" | Bulk removal triggered |
| 7 | Verify AI section | All AI participant chips are REMOVED |
| 8 | Verify AI section is empty or shows "No AI participants" | Section cleared |
| 9 | Click "Restrict access" to confirm | Operation succeeds, wizard closes |
| 10 | Refresh page | Changes persist |
| 11 | Open conversation | Conversation opens |
| 12 | Try to invoke removed AI agents | Agents NOT available / cannot be @mentioned |

## Expected Final State

- All AI participants removed from conversation
- Removal persists after refresh
- Cannot invoke removed AI agents

## Teardown

- None required
