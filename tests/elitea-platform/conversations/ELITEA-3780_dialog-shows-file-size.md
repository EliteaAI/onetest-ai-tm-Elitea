---
id: ELITEA-3780
title: "Verify Dialog Shows Correct File Size For Attachments"
priority: medium
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, feat:chat, feat:export, ui, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3780: Verify Dialog Shows Correct File Size For Attachments

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the export dialog correctly displays the total file count and cumulative size for conversations with attachments.

**Coverage:**
- File count displayed next to "With attachments" option
- Total size calculated and displayed
- Size shown in appropriate units (KB, MB, GB)
- Format matches expected pattern: "(N files · X.XX MB)"

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with attachments (known file sizes)
- User is the conversation creator

## Test Data

- Conversation with 3 attachments:
  - image.png: ~500 KB
  - doc.pdf: ~1.2 MB
  - file.docx: ~300 KB
- Expected total: 3 files, ~2 MB

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Calculate expected total size | ~2 MB (500 KB + 1.2 MB + 300 KB = 2 MB) |
| 2 | Navigate to Chats section | Chat list displays |
| 3 | Right-click conversation with attachments | Context menu with "Export" |
| 4 | Click "Export" | Dialog opens |
| 5 | Locate "With attachments" radio button | Radio button visible |
| 6 | Verify attachment info displayed next to radio button | Text shows: "(3 files · X.XX MB)" |
| 7 | Verify file count | "(3 files · ...)" displayed |
| 8 | Verify size shown | Size value displayed: "2 MB" or "2.0 MB" or similar |
| 9 | Verify format | Format matches: "(N files · X.XX MB)" or "(N files · X.XX KB)" |
| 10 | Verify size accuracy | Displayed size (~2 MB) matches expected total (within reasonable rounding) |
| 11 | Verify units appropriate | Units correct for size: KB for < 1 MB, MB for 1-1000 MB, GB for > 1000 MB |
| 12 | Test with small files conversation (if available) | Files < 1 MB show in KB: e.g., "(2 files · 750 KB)" |
| 13 | Test with large files conversation (if available) | Files > 1 MB show in MB: e.g., "(5 files · 15.5 MB)" |

## Expected Final State

- File count and size displayed correctly
- Appropriate units used (KB/MB)
- Format matches pattern
- Size accurate

## Pass/Fail Criteria

**Pass:**
- File count displayed correctly (e.g., "3 files")
- Total size displayed and accurate (e.g., "2 MB")
- Appropriate units (KB/MB/GB) for file size
- Format matches: "(N files · X.XX MB/KB)"

**Fail:**
- File count wrong or missing
- Size incorrect or missing
- Wrong units (e.g., bytes instead of MB)
- Format doesn't match expected pattern

## Postconditions

- Dialog remains functional
- Size information helps user make informed choice
