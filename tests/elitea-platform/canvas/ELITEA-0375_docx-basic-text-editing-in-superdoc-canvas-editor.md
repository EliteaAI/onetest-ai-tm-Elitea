---
id: ELITEA-0375
title: "DOCX - Basic Text Editing in SuperDoc Canvas Editor"
priority: critical
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0375: DOCX - Basic Text Editing in SuperDoc Canvas Editor

**Module:** Canvas · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that basic text operations (type, delete, paste) work correctly inside the SuperDoc editor in Canvas.

**Coverage:**
- Typing new text into the document
- Deleting existing text
- Pasting text from clipboard

## Preconditions

- Logged in to {{base_url}}
- DOCX file open in Canvas SuperDoc editor (from Artifacts or Chat)

## Test Data

- Insert text: `"Test edit [timestamp]"` (e.g. `"Test edit 2026-03-10"`)
- Text to delete: first word of the first paragraph

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into a paragraph in the SuperDoc editor and type new text: `Test edit [timestamp]` | Text appears at the cursor position immediately |
| 2 | Select a word using the cursor and press Delete or Backspace | Selected text is removed from the document |
| 3 | Copy text from another source (e.g. clipboard), click in the editor, and press Ctrl+V (or Cmd+V) | Pasted text appears at the cursor position |

## Expected Final State

Pasted text appears at the cursor position

## Pass/Fail Criteria

**Pass:**
- All three operations (type, delete, paste) are reflected immediately in the editor

**Fail:**
- Text does not appear when typed
- Deletion does not remove selected text
- Paste does not insert content from clipboard
