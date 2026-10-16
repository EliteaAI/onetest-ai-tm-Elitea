---
id: ELITEA-3866
title: "Download MDX File from Three-Dot Menu"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3866: Download MDX File from Three-Dot Menu

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify Download option downloads MDX file to local machine

## Preconditions

- MDX file is open in Canvas

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Canvas | File opens |
| 2 | Click three-dot menu (⋮) | Menu opens |
| 3 | Click "Download" option | Download initiates |
| 4 | Check browser downloads | File downloaded |

## Expected Results

- File downloads to local machine
- Downloaded file has correct name with .mdx extension
- Downloaded file contains correct MDX source code
- File can be opened in text editor and is valid MDX

## Pass/Fail Criteria

**Pass:**
- File downloads successfully
- Correct filename and extension
- Content is valid and complete

**Fail:**
- Download fails
- Wrong filename or extension
- Content is corrupted or incomplete
