---
id: ELITEA-2726
title: "HTML with special characters renders correctly"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file with special characters is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test characters | Accented letters, trademark, copyright, currency symbols, emojis |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate HTML with special characters | Test file contains UTF-8 characters |
| 2 | Open the file in Preview mode | File opens in Canvas |
| 3 | Observe special character rendering | Characters display correctly |
| 4 | Verify accented letters | Accents render properly |
| 5 | Verify symbols | Symbols display correctly |
| 6 | Verify emojis if present | Emojis render correctly |
| 7 | Switch to Raw mode | Source code displays |
| 8 | Verify character representation in source | Characters show correctly |
| 9 | Edit and save a special character | Change saves correctly |

## Expected Final State

- All special characters display correctly in Preview mode
- UTF-8 encoding is properly handled
- Characters do not appear as garbled text or question marks
- Raw mode shows correct character representation
- Editing preserves special characters

## Pass/Fail Criteria

**Pass:**
- Special characters display correctly in Preview
- UTF-8 encoding handled properly
- No garbled text or question marks
- Editing preserves characters

**Fail:**
- Characters appear garbled or as question marks
- Encoding issues cause display problems
- Characters lost during editing
