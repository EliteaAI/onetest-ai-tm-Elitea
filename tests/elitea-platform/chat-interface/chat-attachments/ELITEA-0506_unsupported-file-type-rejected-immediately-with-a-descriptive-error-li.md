---
id: ELITEA-0506
title: "Unsupported file type rejected immediately with a descriptive error listing allowed extensions"
priority: medium
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0506: Unsupported file type rejected immediately with a descriptive error listing allowed extensions

**Module:** Chat Attachments · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attaching a file with an extension not in any supported category (images, documents, data, code) is rejected immediately with a clear, descriptive error message — not a generic failure or silent drop — and the file does not appear in the attachment input.

**Coverage:**
- Unsupported file types rejected without appearing in the input
- Error message is descriptive — identifies the file name and indicates unsupported type
- Error does not just say "upload failed" — it references the file type or lists allowed types
- Applies to multiple unsupported formats (.exe, .parquet, .zip)
- File not stored in `attachments` bucket after rejection

## Preconditions

- Logged into ELITEA at {{base_url}}
- Test files with unsupported extensions available locally

## Test Data

- `test.exe` (executable — not in any supported category)
- `data.parquet` (columnar data format — not supported)
- `archive.zip` (archive — not supported)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation → click the paperclip → attempt to attach `test.exe` via the file browser | File is rejected; a descriptive error message appears naming `test.exe` and indicating the type is unsupported; `test.exe` does NOT appear as a thumbnail |
| 2 | Inspect the error message text | Error is descriptive — not just 'upload failed'; it references the file name and/or the unsupported extension |
| 3 | Attempt to attach `data.parquet` (via file browser or drag-and-drop) | File rejected with a descriptive error; no thumbnail added to input |
| 4 | Attempt to attach `archive.zip` | File rejected with a descriptive error; no thumbnail added |
| 5 | Verify the chat input area after all three attempts | Input area is empty — no thumbnails for any of the three rejected files; the input is unchanged |

## Expected Final State

Input area is empty — no thumbnails for any of the three rejected files; the input is unchanged

## Pass/Fail Criteria

**Pass:**
- All 3 unsupported files rejected with descriptive error messages
- None of the rejected files appear as thumbnails in the input
- Error messages reference the file name or type — not generic

**Fail:**
- Any unsupported file accepted silently or added to input
- Error message is generic (e.g., "Upload failed" with no detail)
- File appears in `attachments` bucket after rejection
