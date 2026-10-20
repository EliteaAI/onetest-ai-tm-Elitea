---
id: ELITEA-3766
title: "Export Conversation With Documents - Verify Documents in ZIP"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3766: Export Conversation With Documents - Verify Documents in ZIP

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations with document attachments export correctly with documents preserved in the ZIP archive.

**Coverage:**
- Document files are included in ZIP export
- Documents maintain original filename and format
- Documents can be opened in respective applications
- Document content remains intact and readable

## Preconditions

- Logged in to {{base_url}}
- Conversation with at least 2 document attachments (.pdf, .docx, .txt, .xlsx, etc.)
- User is the conversation creator

## Test Data

- Conversation with 2-3 document files (different formats: PDF, DOCX, TXT, XLSX)
- Known document filenames: e.g., "report.pdf", "notes.docx", "data.xlsx"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify conversation with document attachments | Conversation with documents visible |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Verify "With attachments" shows document count | e.g., "(3 files · 2.5 MB)" displayed |
| 6 | Select "With attachments" | Radio button selected |
| 7 | Click "Export" | ZIP downloads |
| 8 | Extract ZIP archive | Extraction succeeds |
| 9 | Navigate to attachments folder in ZIP | Attachments folder visible |
| 10 | Verify all document files present | report.pdf, notes.docx, data.xlsx found |
| 11 | Verify original filenames preserved | Filenames match original documents |
| 12 | Verify original formats preserved | Extensions intact: .pdf, .docx, .txt, .xlsx |
| 13 | Open report.pdf | Document opens correctly in PDF reader |
| 14 | Open notes.docx | Document opens correctly in word processor |
| 15 | Open data.xlsx | Document opens correctly in spreadsheet application |
| 16 | Verify document content intact | Text, formatting, and data readable and unchanged |
| 17 | Verify document file sizes match original | File sizes match |

## Expected Final State

- ZIP archive contains all document files in attachments folder
- Documents have original filenames and formats
- Documents can be opened in respective applications
- Document content is intact and readable

## Pass/Fail Criteria

**Pass:**
- All documents present in ZIP/attachments folder
- Original filenames and formats preserved (.pdf, .docx, .txt, .xlsx)
- Documents open correctly in respective applications
- Content intact and readable
- File sizes match originals

**Fail:**
- Documents missing from ZIP
- Filenames changed or formats altered
- Documents corrupted or cannot be opened
- Content lost or unreadable
- File sizes significantly different

## Postconditions

- Original conversation with documents unchanged
- Documents remain accessible in conversation
