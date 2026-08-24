---
id: ELITEA-2705
title: "Switch from Preview to Raw mode"
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
- HTML file is open in Canvas in Preview mode

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_2_between_1_3mb_structured.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an HTML file in Canvas (Preview mode is default) | File displays in Preview mode with rendered HTML |
| 2 | Click on "Raw" tab | Canvas view switches to Raw mode |
| 3 | Observe the display content | HTML source code is displayed |
| 4 | Verify syntax highlighting is applied | HTML tags are colored distinctly |
| 5 | Verify line numbers are visible | Line numbers appear on the left side of the editor |

## Expected Final State

- Canvas is in Raw mode showing HTML source code
- Code has syntax highlighting (HTML tags colored)
- Line numbers are visible
- Code is properly formatted and readable
- Same file name and path remain in header

## Pass/Fail Criteria

**Pass:**
- Canvas switches to Raw mode on tab click
- HTML source code is displayed (not rendered)
- Syntax highlighting is applied to HTML tags
- Line numbers are visible
- File header information remains unchanged

**Fail:**
- Tab click does not switch modes
- Source code is not displayed or is unreadable
- No syntax highlighting is applied
- Line numbers are missing
