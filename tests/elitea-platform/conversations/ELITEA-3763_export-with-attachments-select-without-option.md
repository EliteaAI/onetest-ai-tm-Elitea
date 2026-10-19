---
id: ELITEA-3763
title: "Export Conversation With Attachments - Select Without Attachments Option"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3763: Export Conversation With Attachments - Select Without Attachments Option

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a conversation has attachments but "Without attachments" is selected, only the JSON file is exported.

**Coverage:**
- Export dialog shows attachment information for conversations with attachments
- "Without attachments" option explicitly excludes attachments from export
- Only JSON file is downloaded when "Without attachments" is selected
- Attachments are not included even though they exist in the conversation

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with text messages AND attachments (images/documents)
- User is the conversation creator

## Test Data

- Conversation with at least 3 messages and 2 attachments (images or documents)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays with conversations |
| 2 | Right-click on conversation with attachments | Context menu appears with "Export" option |
| 3 | Click "Export" | Dialog opens showing both radio options |
| 4 | Verify "With attachments" option shows file count and size | e.g., "(2 files · 1.28 MB)" displayed next to radio button |
| 5 | Verify "Without attachments" radio button is present | Radio button visible |
| 6 | Select "Without attachments" radio button | Radio button becomes selected |
| 7 | Verify help text changes | Text reads: "Only chat messages will be exported as a JSON file." |
| 8 | Click "Export" button | Download initiates |
| 9 | Check downloads folder | JSON file downloads (NOT a ZIP archive) |
| 10 | Verify filename | Filename follows pattern: Conversation_[Name]_YYYY-MM-DD.json |
| 11 | Open JSON file in text editor | JSON contains messages but no attachment files |
| 12 | Verify JSON structure | Messages array present with text content |
| 13 | Verify no embedded attachments in JSON | No base64-encoded files or attachment data |
| 14 | Verify success notification | "Chat exported successfully" banner appears |

## Expected Final State

- Only JSON file downloaded (not ZIP)
- JSON contains messages but no attachment files
- Attachments remain in original conversation but not in export
- Success notification displayed

## Pass/Fail Criteria

**Pass:**
- Dialog correctly shows attachment count for "With attachments" option
- Selecting "Without attachments" downloads only JSON file
- No ZIP archive created
- Attachments not included in export
- Success notification appears

**Fail:**
- ZIP archive downloads instead of JSON
- Attachments included in export despite "Without attachments" selection
- Download fails or incorrect file type
- No success notification

## Postconditions

- Original conversation with attachments unchanged
- Attachments remain accessible in conversation
