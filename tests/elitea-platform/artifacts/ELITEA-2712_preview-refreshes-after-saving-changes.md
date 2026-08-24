---
id: ELITEA-2712
title: "Preview refreshes after saving changes in Raw mode"
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
| Test file | test_file_2_between_1_3mb_structured.htm |
| Original text | Executive Dashboard |
| Modified text | TEST Dashboard |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas and switch to Raw mode | Raw mode displays HTML source |
| 2 | Locate "Executive Dashboard" text in the HTML | Text is found in the source |
| 3 | Change "Executive Dashboard" to "TEST Dashboard" | Text is modified in editor |
| 4 | Click Save button | Changes are saved |
| 5 | Switch to Preview mode | Preview mode displays |
| 6 | Locate the dashboard section | Dashboard section is visible |
| 7 | Verify "TEST Dashboard" is displayed | Modified text appears in Preview |

## Expected Final State

- Preview mode displays the updated content
- Change is visible in rendered HTML
- No stale cache or old content is displayed

## Pass/Fail Criteria

**Pass:**
- Preview mode shows "TEST Dashboard" after save
- Changes reflect immediately
- Content is properly rendered with the update

**Fail:**
- Preview still shows "Executive Dashboard"
- Changes are not reflected in Preview
- Page requires manual refresh to see changes
