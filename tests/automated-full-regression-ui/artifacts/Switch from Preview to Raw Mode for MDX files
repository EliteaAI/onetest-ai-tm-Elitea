---
id: ELITEA-2311
title: "Switch from Preview to Raw Mode"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2311: Switch from Preview to Raw Mode

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can switch from Preview mode to Raw mode to view MDX source code

## Preconditions

- MDX file is open in Canvas in Preview mode

## Test Data

- File: `test_file_1_under_1mb.mdx`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With MDX file open in Preview mode | File is displayed with rendered content |
| 2 | Click on "Raw" tab | Canvas switches to Raw mode |
| 3 | Observe the display changes | Source code is visible |
| 4 | Note the code presentation | Syntax highlighting is applied |

## Expected Results

- Canvas switches to Raw mode immediately
- MDX source code is displayed in code editor
- Code has syntax highlighting (Markdown and MDX/JSX syntax colored)
- Line numbers are visible on the left (1, 2, 3...)
- Code is properly formatted and readable
- Same file name and path remain in header
- MDX-specific syntax (imports, exports, JSX) is highlighted appropriately

## Pass/Fail Criteria

**Pass:**
- Mode switch occurs instantly
- Source code displays with proper syntax highlighting
- Line numbers and formatting are correct

**Fail:**
- Mode switch fails or shows error
- Source code is not displayed
- No syntax highlighting applied
- Line numbers missing
