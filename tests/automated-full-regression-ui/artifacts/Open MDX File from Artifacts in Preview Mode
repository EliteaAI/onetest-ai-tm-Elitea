---
id: ELITEA-2310
title: "Open MDX File from Artifacts in Preview Mode"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2310: Open MDX File from Artifacts in Preview Mode

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify MDX files open correctly from Artifacts bucket in Preview mode by default

## Preconditions

- User is logged into NEXT environment
- MDX test files exist in Artifacts: `Elitea S3 storage > mdx` folder
- User has read access to Artifacts

## Test Data

- Bucket: `Elitea S3 storage`
- Folder: `mdx`
- File: `test_file_1_under_1mb.mdx` (4.9 KB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log into https://next.elitea.ai/app/ | User successfully logged in |
| 2 | Navigate to Artifacts section (left sidebar) | Artifacts page opens |
| 3 | Select bucket: "Elitea S3 storage" | Bucket expands showing folders |
| 4 | Navigate to folder: mdx | Folder contents display |
| 5 | Click on file: `test_file_1_under_1mb.mdx` | Canvas opens with file |
| 6 | Observe the Canvas display | File opens in Preview mode |

## Expected Results

- File opens in Canvas/File Preview
- "Preview" tab is selected and active by default
- File type indicator displays: "MDX (detected)"
- MDX content renders correctly with formatted Markdown
- Main heading visible: "Test MDX File 1 - Under 1MB"
- Subheadings render: "Introduction", "Content Section"
- Formatted text and paragraphs are visible
- "Raw" tab is visible and clickable next to Preview
- File path breadcrumb shows: mdx > test_file_1_under_1mb.mdx
- Three-dot menu (⋮) is visible in top-right
- Close button (X) is visible

## Pass/Fail Criteria

**Pass:**
- MDX file opens in Canvas with Preview mode active by default
- File type correctly identified as "MDX (detected)"
- Content renders properly with Markdown formatting

**Fail:**
- File fails to open
- Opens in Raw mode instead of Preview
- File type is not identified
- Content does not render or shows errors
