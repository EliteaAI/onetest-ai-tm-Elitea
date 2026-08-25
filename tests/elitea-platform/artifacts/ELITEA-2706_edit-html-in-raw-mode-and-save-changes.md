---
id: ELITEA-2706
title: "Edit HTML in Raw mode and save changes"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file is open in Raw mode
- User has write permission to the Artifacts bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_2_between_1_3mb_structured.htm |
| Original title | Comprehensive Test Report 2 - Between 1MB and 3MB |
| Modified title | TEST EDIT - Modified Title |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas and switch to Raw mode | Raw mode displays HTML source code |
| 2 | Locate the `<title>` tag (around line 6) | Title tag is visible in the code |
| 3 | Click in the editor and modify the title text to "TEST EDIT - Modified Title" | Text is editable, cursor appears in editor |
| 4 | Observe the Save button state | Save button becomes active (changes from gray to purple) |
| 5 | Click "Save" button | Changes are saved |
| 6 | Switch to Preview mode | Preview mode displays |
| 7 | Verify the title change is reflected | Updated title is visible in rendered HTML |

## Expected Final State

- Changes are saved successfully without errors
- Preview mode shows the updated title in the rendered HTML
- No error messages appear
- Save button returns to inactive state after saving

## Pass/Fail Criteria

**Pass:**
- Code editor allows text editing
- Save button activates after modification
- Save operation completes without errors
- Preview mode reflects the saved changes

**Fail:**
- Editor does not allow editing
- Save button remains inactive after changes
- Error message appears when saving
- Preview mode does not show updated content
