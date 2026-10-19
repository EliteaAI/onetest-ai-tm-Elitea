---
id: ELITEA-3774
title: "Export Conversation From Folder"
priority: medium
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:folders, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3774: Export Conversation From Folder

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that conversations organized in folders can be exported successfully.

**Coverage:**
- Conversations in folders can be exported
- Export functionality works for folder-organized conversations
- Folder information may be included in export metadata
- Conversation data complete regardless of folder location

## Preconditions

- Logged in to {{base_url}}
- Conversations organized in folders (e.g., "Bugs", "Projects", custom folders)
- User is the conversation creator

## Test Data

- Conversation in a folder (e.g., "Bugs" folder) with 5+ messages
- Folder name: "Bugs"
- Conversation name: "Bug Investigation"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list with folders displayed |
| 2 | Navigate to a folder (e.g., "Bugs") | Folder expands showing conversations inside |
| 3 | Identify conversation in folder | Conversation visible within folder |
| 4 | Right-click on conversation in folder | Context menu with "Export" appears |
| 5 | Click "Export" | Dialog opens |
| 6 | Verify conversation name shown correctly | Name matches conversation in folder |
| 7 | Click "Export" | File downloads |
| 8 | Verify filename | Filename: Conversation_Bug_Investigation_YYYY-MM-DD.json |
| 9 | Open exported JSON file | JSON structure visible |
| 10 | Verify all messages from conversation included | All messages present |
| 11 | Check for folder information in metadata (optional) | JSON may include folder path/name in metadata (if feature supported) |
| 12 | Verify conversation data complete | All conversation data exported regardless of folder location |
| 13 | Verify success notification | "Chat exported successfully" appears |
| 14 | After export, verify conversation still in folder | Conversation remains organized in folder |

## Expected Final State

- Folder conversation exported successfully
- Conversation data complete
- Folder organization unchanged
- Success notification displayed

## Pass/Fail Criteria

**Pass:**
- Conversation in folder exports successfully
- All messages included
- Filename correct
- Optional: Folder metadata included
- Success notification appears

**Fail:**
- Export fails for folder conversations
- Messages missing or incomplete
- Download error
- Folder organization disrupted
- No success notification

## Postconditions

- Conversation remains in folder
- Folder organization unchanged
- Conversation accessible
