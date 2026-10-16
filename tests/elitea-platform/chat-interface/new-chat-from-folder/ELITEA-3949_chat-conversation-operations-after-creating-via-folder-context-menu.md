---
id: ELITEA-3949
title: "Chat – Conversation operations after creating via folder context menu"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6]
requirements: [EliteaAI/elitea_issues#1604]
---

# ELITEA-3949: Chat – Conversation operations after creating via folder context menu

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that conversations created via folder context menu support all standard operations: works in pinned folders, can be renamed, deleted, and the folder containing such conversation can be deleted.

---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on the Chats section
- At least one pinned folder and one regular folder exist in the Chats section

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test message 1 | Conversation in pinned folder |
| Test message 2 | Conversation for rename test |
| New name | Renamed Conversation |
| Test message 3 | Conversation in folder to delete |

---

## Steps

### Part 1: Pinned folder

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click three-dot icon (⋮) on the folder row → click "New chat" | New conversation opens |
| 2 | Send message: "Conversation in pinned folder" and wait for auto-naming | Conversation appears in the pinned folder |
| 3 | Verify folder remains pinned (appears at top with pin indicator) | Folder is still pinned after conversation creation |

### Part 2: Rename conversation

| # | Action | Expected Result |
|---|--------|-----------------|
| 4 | Click three-dot icon (⋮) on the folder row → click "New chat" | New conversation opens |
| 5 | Send message: "Conversation for rename test" and wait for auto-naming | Conversation appears in the folder |
| 6 | Click three-dot icon (⋮) on the conversation → select "Rename" | Rename input field appears |
| 7 | Enter "Renamed Conversation" and save | Conversation name is updated; conversation remains in the folder |

### Part 3: Delete conversation

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Click three-dot icon (⋮) on the renamed conversation → select "Delete" | Delete confirmation appears |
| 9 | Confirm deletion | Conversation is removed from the folder |

### Part 4: Delete folder with conversation

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Create a new folder, click three-dot icon (⋮) on the folder row → click "New chat" | New conversation opens |
| 11 | Send message: "Conversation in folder to delete" and wait for auto-naming | Conversation appears in the folder |
| 12 | Click three-dot icon (⋮) on the folder → select "Delete" | Delete confirmation appears (may warn about contents) |
| 13 | Confirm deletion | Folder and conversation inside are deleted; no orphaned conversations in date-based sections |

---

## Expected Final State

- Conversations created via folder context menu support all standard operations
- Pinned folder state is preserved after creating conversation
- Rename and delete operations work correctly
- Deleting folder also deletes conversations inside without orphaning them

---

## Pass/Fail Criteria

**Pass:**
- Conversation creation works in pinned folder; folder remains pinned
- Conversation can be renamed successfully
- Conversation can be deleted successfully
- Folder with conversation can be deleted; no orphaned conversations remain

**Fail:**
- Folder becomes unpinned after conversation creation
- Rename or delete operations fail
- Orphaned conversations appear after folder deletion
