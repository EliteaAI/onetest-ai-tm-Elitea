---
id: ELITEA-3771
title: "Export Conversation From Private Project"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:projects, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3771: Export Conversation From Private Project

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations in Private projects can be exported successfully.

**Coverage:**
- Private project conversations can be exported
- Export functionality works in Private project context
- Exported data isolated to Private project conversation
- No data leakage from other projects

## Preconditions

- Logged in to {{base_url}}
- In Private project context
- At least one conversation exists in Private project
- User is the conversation creator

## Test Data

- Conversation in Private project with 5+ messages
- Conversation name: "Private Project Test"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Private project | Private project selected (verify project indicator/label) |
| 2 | Go to Chats section | Private project conversations listed |
| 3 | Verify conversation is in Private project | Conversation visible in Private context |
| 4 | Right-click on a private conversation | Context menu with "Export" appears |
| 5 | Click "Export" | Dialog opens |
| 6 | Verify dialog shows correct conversation name | Conversation name displayed matches |
| 7 | Click "Export" | File downloads |
| 8 | Verify filename includes conversation identifier | Filename: Conversation_Private_Project_Test_YYYY-MM-DD.json |
| 9 | Open exported JSON file | JSON structure visible |
| 10 | Verify all messages from private conversation included | All messages present |
| 11 | Verify project context metadata (if included) | JSON may include project reference showing "Private" |
| 12 | Verify no data leakage from other projects | Only this conversation's data present, no other project data |
| 13 | Verify success notification | "Chat exported successfully" appears |

## Expected Final State

- Private project conversation exported successfully
- Data isolated to that conversation only
- Success notification displayed
- Original conversation unchanged

## Pass/Fail Criteria

**Pass:**
- Export succeeds in Private project context
- All conversation messages exported
- Data isolated (no leakage from other projects)
- Filename correct
- Success notification appears

**Fail:**
- Export fails or unavailable in Private project
- Messages missing or incomplete
- Data from other projects included
- Download error
- No success notification

## Postconditions

- Private project conversation unchanged
- User can continue working in Private project
