---
id: ELITEA-2713
title: "Copy Content from three-dot menu"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file is open in Canvas

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | Any HTML file from Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas (any mode) | File is displayed in Canvas |
| 2 | Click three-dot menu in top-right corner | Menu dropdown appears |
| 3 | Observe menu options | Menu shows available actions |
| 4 | Click "Copy Content" option | Content is copied to clipboard |
| 5 | Open a text editor (e.g., Notepad, VS Code) | Text editor is ready |
| 6 | Paste content (Ctrl+V / Cmd+V) | Content is pasted |
| 7 | Compare pasted content with Raw mode view | Content matches |

## Expected Final State

- Full HTML source code is copied to clipboard
- Pasted content is identical to Raw mode view

## Pass/Fail Criteria

**Pass:**
- Three-dot menu shows "Copy Content", "Download", and "Delete" options
- Copy Content copies full HTML source code
- Pasted content matches the Raw mode view exactly

**Fail:**
- Copy Content option is missing from menu
- Copying fails or shows error
- Pasted content is incomplete or corrupted
