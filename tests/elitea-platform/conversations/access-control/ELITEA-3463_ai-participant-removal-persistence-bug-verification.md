---
id: ELITEA-3463
title: "AI Participant Removed from List Immediately After Deletion"
priority: high
type: regression
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, ai-participants, bug-verification, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283, EliteaAI/elitea_issues#6795]
---
# ELITEA-3463: AI Participant Removed from List Immediately After Deletion

**Module:** Conversations · **Priority:** High · **Type:** Regression / Bug Verification

**Objective:** Verify that AI participants are removed from the participant list immediately after deletion via Restrict Access wizard (Bug #6795 verification).

**Bug Reference:** [#6795](https://github.com/EliteaAI/elitea_issues/issues/6795) - Deleted AI Participant Persists in Chat Participant List After Removal via Restrict Access Wizard

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A conversation exists with 2+ AI participants
- User has permissions to access the "Restrict Access" wizard

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| AI Participants | 2+ AI agents |
| Bug | #6795 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat that has more than one AI participant | Chat opens with AI participants visible |
| 2 | Note the AI participants in the conversation | AI-Agent-1 and AI-Agent-2 (example) visible |
| 3 | Open the "Restrict Access" wizard | Wizard shows both AI participants |
| 4 | Delete one AI participant (click x on chip) | AI removed from selection in wizard |
| 5 | Click "Restrict access" to confirm/save | Wizard closes |
| 6 | IMMEDIATELY check the chat's participant list | Deleted AI should NOT appear |
| 7 | Do NOT refresh the page | Observe participant list |
| 8 | Refresh page | Deleted AI still not present (persisted) |

## Expected Final State

- AI participant removed immediately without page refresh
- Participant list accurately reflects the change

## Pass/Fail Criteria

**Pass:**
- Step 6: Deleted AI participant is NOT in the participant list immediately

**Fail (Bug #6795):**
- Step 6: Deleted AI participant still appears in the chat's participant list until refresh

## Teardown

- None required
