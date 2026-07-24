---
id: ELITEA-2325
title: "Medium-Sized MDX File Performance"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, nfr:performance, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2325: Medium-Sized MDX File Performance

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify medium MDX files (100KB-1MB) open and perform well

## Preconditions

- Artifacts bucket contains medium-sized MDX files

## Test Data

- Files: `3.mdx` (470 B), `sample-made-up-content.mdx` (525 B)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts > mdx folder | Folder opens |
| 2 | Open file `3.mdx` or `sample-made-up-content.mdx` | File opens |
| 3 | Measure time to open | Opens quickly |
| 4 | Switch between Preview and Raw modes | Switching is smooth |
| 5 | Scroll through the document in both modes | Scrolling is responsive |
| 6 | Make edits in Raw mode | Editing is responsive |

## Expected Results

- File opens within acceptable time (< 3 seconds)
- Preview mode renders without lag
- Raw mode displays source code without delay
- Switching modes is smooth (< 1 second)
- Scrolling is responsive in both modes
- Editing is responsive
- No performance degradation

## Pass/Fail Criteria

**Pass:**
- File opens quickly (< 3 seconds)
- Mode switching is fast (< 1 second)
- No lag or performance issues

**Fail:**
- Slow loading (> 3 seconds)
- Mode switching is slow or laggy
- Performance degradation observed
