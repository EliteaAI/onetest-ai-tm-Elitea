---
id: ELITEA-3871
title: "Dark Theme Compatibility for MDX Content"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, nfr:ui, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3871: Dark Theme Compatibility for MDX Content

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify MDX files are readable in Dark theme

## Preconditions

- Elitea UI is set to Dark theme

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Elitea UI to Dark theme (Settings > Theme > Dark) | Theme changes |
| 2 | Navigate to Artifacts > mdx folder | Folder opens |
| 3 | Open an MDX file | File opens |
| 4 | Observe text visibility in Preview mode | Text is readable |
| 5 | Switch to Raw mode and observe | Code is readable |

## Expected Results

- Text is clearly visible and readable in Preview mode
- Text color contrasts well with dark background
- Code blocks have appropriate dark theme styling
- No black-on-black or invisible text issues
- Raw mode has dark theme syntax highlighting
- Content is fully readable without straining

## Pass/Fail Criteria

**Pass:**
- All text readable in dark theme
- Good contrast and visibility
- No display issues

**Fail:**
- Text invisible or hard to read
- Poor contrast
- Display issues in dark theme
