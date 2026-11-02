---
id: ELITEA-3157
title: "Verify Canvas API renders 2D graphics inside the preview iframe"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | `canvas-test.html` — draws a rectangle and text label via `getContext('2d')` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `canvas-test.html` and open in Preview mode | Canvas element is visible |
| 2 | Observe the canvas content | A colored rectangle and text label are drawn |
| 3 | Confirm no blank canvas | Canvas is not blank/empty |

## Expected Final State

Canvas 2D rendering works correctly inside the sandboxed preview iframe.

## Pass/Fail Criteria

**Pass:**
- Rectangle and text label are visibly drawn on the canvas

**Fail:**
- Canvas remains blank or rendering throws an error
