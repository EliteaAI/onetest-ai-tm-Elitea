---
id: ELITEA-3779
title: "Verify Export Option Appears In Conversation Context Menu"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, feat:chat, feat:export, ui, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3779: Verify Export Option Appears In Conversation Context Menu

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Export" option is visible and accessible in the conversation context menu for conversations the user created.

**Coverage:**
- "Export" option present in context menu
- Option positioned correctly among other menu items
- Option enabled (not grayed out)
- Option accessible via right-click
- Clear labeling and iconography

## Preconditions

- Logged in to {{base_url}}
- At least one conversation exists that user created
- User is the conversation creator

## Test Data

- Conversation created by current user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list visible |
| 2 | Locate a conversation created by user | Conversation visible in list |
| 3 | Hover over the conversation | Hover state indicated (highlight or focus) |
| 4 | Right-click on the conversation | Context menu appears |
| 5 | Verify context menu options present | Menu displays with multiple options |
| 6 | Locate "Export" option in menu | "Export" option visible |
| 7 | Verify menu items order | Options include: Rename, Move to, Playback, Duplicate, **Export**, Share externally, Pin on top, Delete |
| 8 | Verify "Export" option positioning | "Export" appears between other options (as shown in reference screenshots) |
| 9 | Verify "Export" is enabled | Option not grayed out, clickable |
| 10 | Verify "Export" label clarity | Text reads "Export" clearly |
| 11 | Check for icon (if present) | Icon present and appropriate for export action |
| 12 | Click elsewhere to close menu | Menu closes without action |
| 13 | Test keyboard navigation (if supported) | Tab or Arrow key to "Export" option works |
| 14 | If keyboard navigation works, press Enter on "Export" | Dialog opens |

## Expected Final State

- "Export" option visible in context menu
- Option enabled and accessible
- Properly positioned among menu items
- Clear labeling

## Pass/Fail Criteria

**Pass:**
- "Export" option visible in conversation context menu
- Option enabled (not disabled/grayed out)
- Properly positioned in menu
- Clear label: "Export"
- Accessible via mouse and keyboard (if keyboard nav supported)

**Fail:**
- "Export" option not visible
- Option disabled or grayed out
- Incorrect positioning
- Unclear or missing label
- Not accessible

## Postconditions

- Conversation unchanged
- Context menu dismisses when not in use
