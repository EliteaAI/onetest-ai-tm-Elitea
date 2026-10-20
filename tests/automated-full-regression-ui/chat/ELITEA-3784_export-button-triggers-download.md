---
id: ELITEA-3784
title: "Verify Export Button Triggers Download"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3784: Verify Export Button Triggers Download

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the "Export" button in the dialog immediately triggers the file download process.

**Coverage:**
- "Export" button visible and enabled
- Clicking Export initiates download
- Download starts immediately (or with progress indicator for large files)
- Dialog closes after initiating export
- Success notification appears
- File completes downloading and is accessible

## Preconditions

- Logged in to {{base_url}}
- At least one conversation exists
- User is the conversation creator
- Browser download settings allow automatic downloads

## Test Data

- Conversation with 5+ messages (for quick download test)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Right-click conversation | Context menu with "Export" |
| 3 | Click "Export" | Dialog opens |
| 4 | Verify "Export" button visible and enabled | Button present and clickable |
| 5 | Select export option (with or without attachments) | Selection made |
| 6 | Click "Export" button | Download initiates |
| 7 | For JSON (small file), verify immediate download | File appears in browser downloads immediately |
| 8 | For ZIP (larger file), verify progress indicator appears | Progress indicator shown: "Exporting chat... N files" |
| 9 | Verify dialog closes after initiating export | Dialog dismisses |
| 10 | Verify success notification appears | Green banner: "Chat exported successfully" |
| 11 | Check browser downloads list | File appears in downloads list |
| 12 | Wait for download to complete | Download finishes (progress reaches 100%) |
| 13 | Verify file is accessible | File can be clicked/opened from downloads |
| 14 | Open/extract downloaded file | File opens or extracts without errors |
| 15 | Verify file content | File is not corrupted, content accessible |

## Expected Final State

- Export button triggers download
- Dialog closes
- Success notification displayed
- File downloads successfully and is usable

## Pass/Fail Criteria

**Pass:**
- Export button triggers immediate download (or shows progress for large files)
- Dialog closes after initiating export
- Success notification appears: "Chat exported successfully"
- File appears in browser downloads
- Download completes successfully
- File is accessible and not corrupted

**Fail:**
- Export button doesn't trigger download
- Dialog doesn't close
- No success notification
- File doesn't appear in downloads
- Download fails or is corrupted
- File cannot be opened

## Postconditions

- Conversation unchanged
- User can export again if needed
- Downloaded file saved to downloads folder
