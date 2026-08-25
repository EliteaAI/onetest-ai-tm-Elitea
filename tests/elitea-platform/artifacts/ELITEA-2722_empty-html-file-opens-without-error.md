---
id: ELITEA-2722
title: "Empty HTML file opens without error"
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
- Empty HTML file exists in Artifacts (0 bytes or only whitespace)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | Empty .html file (0 bytes or whitespace only) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate an empty HTML file in Artifacts | File exists in Artifacts |
| 2 | Click to open the empty file | File opens in Canvas |
| 3 | Observe Preview mode | Preview shows blank/empty content |
| 4 | Switch to Raw mode | Raw mode displays |
| 5 | Observe Raw mode content | Empty editor or whitespace shown |
| 6 | Verify mode switching works | Can switch between modes |
| 7 | Try editing in Raw mode (add HTML content) | Editor accepts input |
| 8 | Save the added content | Content saves successfully |

## Expected Final State

- Empty file opens in Canvas without errors
- Preview mode shows blank content
- Raw mode shows empty editor
- User can add content and save

## Pass/Fail Criteria

**Pass:**
- File opens without errors
- Preview mode shows blank/empty content
- No error messages appear
- Can edit and add content in Raw mode

**Fail:**
- File fails to open
- Error message appears
- Canvas crashes or freezes
- Cannot add content to empty file
