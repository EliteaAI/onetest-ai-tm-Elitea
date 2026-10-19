---
id: ELITEA-3764
title: "Export Conversation With Attachments - ZIP Archive Generated"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3764: Export Conversation With Attachments - ZIP Archive Generated

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting "With attachments" exports a ZIP archive containing JSON + all attachment files.

**Coverage:**
- "With attachments" option generates ZIP archive
- ZIP contains both JSON file and attachments folder
- Progress indicator shows during export
- All attachment files preserved in ZIP

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with messages and at least 2 attachments
- User is the conversation creator

## Test Data

- Conversation with 5 messages and 3 attachments (mix of images and/or documents)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Right-click on conversation with attachments | Context menu with "Export" appears |
| 3 | Click "Export" | Dialog opens |
| 4 | Verify "With attachments" option | Radio button shows "(3 files · X.XX MB)" |
| 5 | Select "With attachments" radio button | Radio button becomes selected |
| 6 | Verify help text | Text reads: "Chat messages and all attached and generated files/images will be exported as a ZIP archive." |
| 7 | Click "Export" button | Progress indicator appears: "Exporting chat... 3 files" |
| 8 | Verify progress bar | Progress bar shows export progress |
| 9 | Wait for export to complete | ZIP file downloads: Conversation_[Name]_YYYY-MM-DD.zip |
| 10 | Verify ZIP file in downloads folder | ZIP file present with correct name |
| 11 | Extract ZIP archive | Extraction succeeds |
| 12 | Verify ZIP contents | Contains: JSON file + attachments folder |
| 13 | Open attachments folder | All 3 attachment files present |
| 14 | Verify attachments maintain original format and filename | Files have original names and extensions |
| 15 | Open JSON file from ZIP | JSON contains messages with attachment references/metadata |
| 16 | Verify success notification | "Chat exported successfully" banner appears |

## Expected Final State

- ZIP archive downloaded successfully
- ZIP contains JSON file + attachments folder
- All attachment files intact with original names
- Success notification displayed

## Pass/Fail Criteria

**Pass:**
- "With attachments" selection triggers ZIP export
- Progress indicator shows during export
- ZIP downloads with correct naming pattern
- ZIP contains both JSON and attachments folder
- All attachments present and intact
- Success notification appears

**Fail:**
- JSON file downloads instead of ZIP
- ZIP missing attachments folder or files
- Progress indicator not shown
- Attachments corrupted or missing
- Download fails or incomplete

## Postconditions

- Original conversation unchanged
- All attachments remain accessible in conversation
