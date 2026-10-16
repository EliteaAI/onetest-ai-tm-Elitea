---
id: ELITEA-3869
title: "File Type Indicator Shows MDX (Detected)"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3869: File Type Indicator Shows MDX (Detected)

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify file type is correctly detected and displayed

## Preconditions

- MDX file is open in Canvas

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any .mdx file from Artifacts | File opens in Canvas |
| 2 | Observe the file type indicator in Canvas header | Indicator visible |
| 3 | Switch to Raw mode | Mode switches |
| 4 | Observe file type indicator again | Still visible |

## Expected Results

- File type shows "MDX (detected)" with dropdown
- Type indicator is visible next to file name
- Indicator appears in both Preview and Raw modes
- Dropdown allows selecting/confirming file type

## Pass/Fail Criteria

**Pass:**
- File type correctly detected as "MDX (detected)"
- Indicator visible in all modes
- Dropdown functional

**Fail:**
- File type not detected or incorrect
- Indicator missing
- Dropdown not functional
