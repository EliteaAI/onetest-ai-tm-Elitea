---
id: ELITEA-0369
title: "DOCX - SuperDoc - Pre-Save Download Returns Original Document"
priority: medium
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0369: DOCX - SuperDoc - Pre-Save Download Returns Original Document

**Module:** Canvas · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that downloading a DOCX file before saving returns the original unmodified file.

**Coverage:**
- Downloading before saving returns the original document (unsaved changes are NOT included)

## Preconditions

- Logged in to {{base_url}}
- DOCX file open in Canvas SuperDoc editor from Artifacts

## Test Data

- File: `test.docx` in bucket `test-docx-bucket`
- Unsaved edit text: `"UNSAVED_CHANGE"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `UNSAVED_CHANGE` into the document in the editor (do NOT click Save) | Text is visible in the editor; Save button is enabled |
| 2 | Click the Download button in the Canvas modal (before saving) | File downloads as a `.docx` |
| 3 | Open the downloaded file in Microsoft Word or LibreOffice | Downloaded file contains the **original** content — `UNSAVED_CHANGE` is NOT present |

## Expected Final State

Downloaded file contains the **original** content — `UNSAVED_CHANGE` is NOT present

## Pass/Fail Criteria

**Pass:**
- Pre-save download returns the original file without unsaved changes

**Fail:**
- Pre-save download includes unsaved changes
