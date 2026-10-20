---
id: ELITEA-3767
title: "Export Conversation With Mixed Attachments - Images and Documents"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3767: Export Conversation With Mixed Attachments - Images and Documents

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations with both images and documents export correctly with all attachment types preserved.

**Coverage:**
- Mixed attachment types (images + documents) export in single ZIP
- All attachment types maintain original format and filename
- No file naming conflicts or duplicates
- JSON metadata includes all attachment types

## Preconditions

- Logged in to {{base_url}}
- Conversation with mixed attachments: at least 1 image + 1 document
- User is the conversation creator

## Test Data

- Conversation with:
  - 2 images: "chart.png", "photo.jpg"
  - 2 documents: "report.pdf", "notes.docx"
- Total: 4 files

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify conversation with mixed attachments | Conversation with images + documents visible |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Verify file count shows total of all attachment types | "(4 files · 2.5 MB)" displayed |
| 6 | Select "With attachments" | Radio button selected |
| 7 | Verify help text confirms ZIP export | Text mentions ZIP archive |
| 8 | Click "Export" | ZIP downloads |
| 9 | Extract ZIP archive | Extraction succeeds |
| 10 | Navigate to attachments folder | Attachments folder visible |
| 11 | Verify all 4 files present | chart.png, photo.jpg, report.pdf, notes.docx all found |
| 12 | Open chart.png | Image displays correctly |
| 13 | Open photo.jpg | Image displays correctly |
| 14 | Open report.pdf | PDF opens in reader |
| 15 | Open notes.docx | Document opens in word processor |
| 16 | Verify no duplicate files or naming conflicts | All files unique with correct names |
| 17 | Verify each file type maintains format | .png, .jpg, .pdf, .docx extensions intact |
| 18 | Open JSON from ZIP | JSON contains metadata for all 4 attachments |
| 19 | Verify attachment references in JSON | Both image and document types referenced |

## Expected Final State

- ZIP contains all mixed attachment types (images + documents)
- All files preserved with original names and formats
- No duplicates or naming conflicts
- JSON includes metadata for all attachment types

## Pass/Fail Criteria

**Pass:**
- ZIP contains all 4 files (2 images + 2 documents)
- Each file type preserved correctly (images display, documents open)
- Original filenames and formats intact
- No duplicates or conflicts
- JSON includes all attachment metadata

**Fail:**
- Any files missing from ZIP
- File types corrupted or wrong format
- Naming conflicts or duplicates
- Files cannot be opened
- JSON missing attachment metadata

## Postconditions

- Original conversation unchanged
- All attachments remain accessible in conversation
