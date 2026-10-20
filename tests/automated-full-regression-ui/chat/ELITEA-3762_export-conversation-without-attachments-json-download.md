---
id: ELITEA-3762
title: "Export Conversation Without Attachments - JSON File Downloaded"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3762: Export Conversation Without Attachments - JSON File Downloaded

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that a conversation without attachments can be exported successfully as a JSON file containing all messages, timestamps, and metadata.

**Coverage:**
- Export option appears in conversation context menu
- Export dialog shows correctly for conversations without attachments
- JSON file is generated and downloaded with proper structure
- File naming follows the pattern: Conversation_[Name]_YYYY-MM-DD.json

## Preconditions

- Logged in to {{base_url}}
- At least one conversation exists with only text messages (no attachments)
- User has permission to export the conversation (conversation creator)

## Test Data

- Conversation: "Test Conversation" with at least 5 text messages
- Conversation should contain messages with different timestamps
- Conversation should include metadata (sender names, message types)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Chats section | Chat list is displayed with existing conversations |
| 2 | Right-click on a conversation without attachments | Context menu appears with options including "Export" |
| 3 | Click "Export" from the context menu | "Export chat" dialog opens showing the conversation name |
| 4 | Verify dialog content | Dialog displays conversation name and "Without attachments" / "With attachments" radio buttons |
| 5 | Confirm "Without attachments" is selected by default | "Without attachments" radio button is selected |
| 6 | Verify help text below radio buttons | Help text reads: "Only chat messages will be exported as a JSON file." |
| 7 | Verify "Cancel" and "Export" buttons are visible | Both buttons are present and enabled |
| 8 | Click "Export" button | Download initiates immediately |
| 9 | Check browser downloads folder | JSON file is downloaded with name pattern: Conversation_[ConversationName]_YYYY-MM-DD.json |
| 10 | Open the downloaded JSON file in a text editor | JSON file contains valid JSON structure |
| 11 | Verify JSON content structure | JSON contains: messages array, timestamps for each message, sender information, metadata |
| 12 | Verify message order in JSON | Messages appear in correct chronological order |
| 13 | Verify timestamps format | Timestamps are in ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ) |
| 14 | Verify no attachments key/array in JSON | No attachments section present (or empty array) |
| 15 | Verify success notification | Green banner appears with message: "Chat exported successfully" |

## Expected Final State

- JSON file downloaded with all conversation messages
- File name matches pattern: Conversation_[Name]_YYYY-MM-DD.json
- JSON contains all messages in correct order with timestamps
- Success notification displayed

## Pass/Fail Criteria

**Pass:**
- Export option visible in context menu for conversation creator
- Export dialog opens with correct radio button selection
- JSON file downloads with correct naming pattern
- JSON structure is valid and contains all messages with timestamps
- Success notification appears after export

**Fail:**
- Export option not visible or disabled
- Export dialog doesn't open or shows incorrect information
- JSON file not downloaded or has incorrect name
- JSON structure invalid or missing messages/timestamps
- No success notification or error occurs

## Postconditions

- Original conversation remains unchanged
- User can perform additional exports without issues
