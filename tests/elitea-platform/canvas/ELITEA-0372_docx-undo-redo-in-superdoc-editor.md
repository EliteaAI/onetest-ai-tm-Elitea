---
id: ELITEA-0372
title: "DOCX - Undo/Redo in SuperDoc Editor"
priority: high
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0372: DOCX - Undo/Redo in SuperDoc Editor

**Module:** Canvas · **Priority:** High · **Type:** Functional

**Objective:** Verify that Undo and Redo operations function correctly in the SuperDoc editor in Canvas.

**Coverage:**
- Undo reverts the last change
- Redo reapplies a reverted change

## Preconditions

- Logged in to {{base_url}}
- DOCX file open in Canvas SuperDoc editor

## Test Data

- Word to type: `UNDO_TEST`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into a paragraph and type `UNDO_TEST` | Word `UNDO_TEST` appears in the editor |
| 2 | Press Ctrl+Z (Undo) or click the Undo toolbar button | `UNDO_TEST` is removed; text reverts to its previous state |
| 3 | Press Ctrl+Y (Redo) or click the Redo toolbar button | `UNDO_TEST` reappears at the original cursor position |

## Expected Final State

`UNDO_TEST` reappears at the original cursor position

## Pass/Fail Criteria

**Pass:**
- Undo removes the typed word
- Redo restores it

**Fail:**
- Undo does not revert the change
- Redo does not reapply the change
- Undo/Redo buttons or keyboard shortcuts are non-functional
