---
id: ELITEA-2319
title: "Preview Refreshes After Saving Changes"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2319: Preview Refreshes After Saving Changes

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify Preview mode updates to show saved changes

## Preconditions

- MDX file is open in Raw mode

## Test Data

- Original heading: "Test MDX File 1"
- Updated heading: "UPDATED Test File"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Raw mode | File opens |
| 2 | Change heading from "Test MDX File 1" to "UPDATED Test File" | Text updated |
| 3 | Save changes | Save completes |
| 4 | Switch to Preview mode | Mode switches |

## Expected Results

- Preview mode displays the updated content
- Change is visible in rendered content (shows "UPDATED Test File")
- No stale cache or old content is displayed
- Preview accurately reflects saved state

## Pass/Fail Criteria

**Pass:**
- Preview shows saved changes immediately
- No caching issues
- Content matches saved state

**Fail:**
- Preview shows old content
- Caching prevents updates
- Content doesn't match saved state
