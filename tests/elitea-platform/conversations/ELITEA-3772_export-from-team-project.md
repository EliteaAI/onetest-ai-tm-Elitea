---
id: ELITEA-3772
title: "Export Conversation From Team Project"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:projects, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3772: Export Conversation From Team Project

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations in Team projects can be exported by the conversation creator.

**Coverage:**
- Team project conversations can be exported by creator
- Export functionality works in Team project context
- Team member information preserved in export
- Exported data isolated to Team project conversation

## Preconditions

- Logged in to {{base_url}}
- In Team project context
- At least one conversation exists in Team project
- User is the conversation creator

## Test Data

- Conversation in Team project with 5+ messages
- Conversation name: "Team Project Discussion"
- Team members involved in conversation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Team project | Team project selected (verify project indicator/label) |
| 2 | Go to Chats section | Team project conversations listed |
| 3 | Verify conversation is in Team project | Conversation visible in Team context |
| 4 | Right-click on a team conversation | Context menu with "Export" appears |
| 5 | Click "Export" | Dialog opens |
| 6 | Verify dialog shows correct conversation name | Conversation name displayed matches |
| 7 | Click "Export" | File downloads |
| 8 | Verify filename | Filename: Conversation_Team_Project_Discussion_YYYY-MM-DD.json |
| 9 | Open exported JSON file | JSON structure visible |
| 10 | Verify all messages from team conversation included | All messages present |
| 11 | Verify team member information preserved | Sender names/IDs for all team members correct |
| 12 | Verify project context metadata (if included) | JSON may include project reference showing "Team" or team name |
| 13 | Verify success notification | "Chat exported successfully" appears |

## Expected Final State

- Team project conversation exported successfully
- Team member data included and correct
- Success notification displayed
- Original conversation unchanged

## Pass/Fail Criteria

**Pass:**
- Export succeeds in Team project context
- All conversation messages exported
- Team member information preserved
- Filename correct
- Success notification appears

**Fail:**
- Export fails or unavailable in Team project
- Messages missing or incomplete
- Team member information incorrect or missing
- Download error
- No success notification

## Postconditions

- Team project conversation unchanged
- All team members retain access
- User can continue working in Team project
