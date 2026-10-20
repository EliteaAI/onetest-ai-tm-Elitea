---
id: ELITEA-3785
title: "Verify Progress Indicator For Large Exports"
priority: medium
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, ui, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3785: Verify Progress Indicator For Large Exports

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a progress indicator is displayed during export of conversations with many attachments or large file sizes.

**Coverage:**
- Progress indicator appears for large exports
- Progress message shows file count
- Progress bar displays and updates
- Indicator disappears when export completes
- User can see progress throughout export

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with 10+ attachments or large attachments (> 10 MB total)
- User is the conversation creator

## Test Data

- Conversation with 20 attachments totaling 50+ MB (or create test conversation with large files)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify conversation with many/large attachments | Conversation visible |
| 3 | Right-click conversation | Context menu with "Export" |
| 4 | Click "Export" | Dialog opens |
| 5 | Verify attachment count and size displayed | Dialog shows: "(20 files · 50 MB)" or similar |
| 6 | Select "With attachments" | Radio button selected |
| 7 | Click "Export" button | Export begins |
| 8 | Verify progress indicator appears | Progress message and bar displayed |
| 9 | Verify progress message text | Text shows: "Exporting chat... 20 files" |
| 10 | Verify progress bar visible | Progress bar displayed below message |
| 11 | Observe progress bar behavior | Bar starts at 0% or near 0% |
| 12 | Monitor progress bar updates | Bar progresses/fills as export proceeds |
| 13 | Verify smooth progression | Bar updates incrementally, not in jumps |
| 14 | Wait for export to complete | Progress reaches 100% |
| 15 | Verify indicator disappears after completion | Progress indicator removed |
| 16 | Verify ZIP file downloads | File appears in downloads folder |
| 17 | Verify success notification | "Chat exported successfully" banner appears |
| 18 | Test with small export (< 1 MB, optional) | Progress may be too fast to see or not shown for very small exports |

## Expected Final State

- Progress indicator shown for large exports
- File count displayed
- Progress bar updates throughout
- Indicator disappears on completion
- Export successful

## Pass/Fail Criteria

**Pass:**
- Progress indicator appears for large exports
- Message shows: "Exporting chat... N files"
- Progress bar visible and updates progressively
- Progress completes (reaches 100%)
- Indicator disappears when export finishes
- ZIP file downloads successfully
- Success notification appears

**Fail:**
- No progress indicator for large exports
- Message missing or incorrect
- Progress bar not visible or doesn't update
- Export hangs or fails
- Indicator doesn't disappear
- File doesn't download

## Postconditions

- Conversation unchanged
- Large export completed successfully
