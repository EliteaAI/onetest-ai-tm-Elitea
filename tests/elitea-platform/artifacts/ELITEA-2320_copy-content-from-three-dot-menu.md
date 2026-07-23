---
id: ELITEA-2320
title: "Copy Content from Three-Dot Menu"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2320: Copy Content from Three-Dot Menu

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify Copy Content option copies MDX source to clipboard

## Preconditions

- MDX file is open in Canvas

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Canvas (any mode) | File opens |
| 2 | Click three-dot menu (⋮) in top-right corner | Menu opens |
| 3 | Click "Copy Content" option | Content copied |
| 4 | Open a text editor (e.g., Notepad) | Editor opens |
| 5 | Paste (Ctrl+V) | Content pastes |

## Expected Results

- Three-dot menu shows "Copy Content", "Download", and "Delete" options
- Clicking "Copy Content" copies MDX source code to clipboard
- Pasted content shows full MDX source code
- Content is identical to Raw mode view
- Markdown and MDX syntax is preserved

## Pass/Fail Criteria

**Pass:**
- Copy Content option works correctly
- Full source code copied to clipboard
- Syntax and formatting preserved

**Fail:**
- Copy Content doesn't work
- Incomplete or corrupted content
- Syntax not preserved
