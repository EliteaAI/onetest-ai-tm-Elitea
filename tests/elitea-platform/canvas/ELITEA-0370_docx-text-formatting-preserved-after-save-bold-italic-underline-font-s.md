---
id: ELITEA-0370
title: "DOCX Text Formatting Preserved After Save [bold / italic / underline / font / size / alignment]"
priority: high
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0370: DOCX Text Formatting Preserved After Save [bold / italic / underline / font / size / alignment]

**Module:** Canvas · **Priority:** High · **Type:** Functional

**Objective:** Verify that text formatting applied in the SuperDoc editor is preserved in the saved DOCX file.

**Coverage (parametrized — each applied and verified after save/reopen):**
- Bold
- Italic
- Underline
- Font family change (e.g. Arial)
- Font size change (e.g. 18pt)
- Paragraph alignment: left, center, right, justify

## Preconditions

- Logged in to {{base_url}}
- DOCX file open in Canvas from Artifacts
- File contains at least one editable paragraph

## Test Data

- Formatting matrix: `[bold, italic, underline, font=Arial, size=18pt, align=center]`
- File: `test.docx` in bucket `test-docx-bucket`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select a text range or paragraph in the SuperDoc editor | Text is selected |
| 2 | Apply each formatting option in sequence via the SuperDoc toolbar: bold, italic, underline, font=Arial, size=18pt, alignment=center | Each formatting change is reflected in the editor immediately after application |
| 3 | Click Save | Save succeeds; success notification appears |
| 4 | Close and reopen the file from Artifacts | All 6 applied formatting options are preserved as saved — bold, italic, underline, font, size, and alignment are all intact |

## Expected Final State

All 6 applied formatting options are preserved as saved — bold, italic, underline, font, size, and alignment are all intact

## Pass/Fail Criteria

**Pass:**
- All 6 formatting types are applied, saved, and survive a reopen

**Fail:**
- Any formatting type is visually lost or reset after save and reopen
