---
id: ELITEA-3151
title: "Verify save and reload of edited HTML file preserves JS execution"
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
- A JS-containing HTML file exists in an artifact bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | Any JS-containing HTML file, edited to change output text (e.g., "Hello" → "Updated") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the file in Canvas mode | File opens successfully |
| 2 | Switch to Raw mode and modify the inline script's output text | Edit is accepted |
| 3 | Click **Save** | Success notification appears |
| 4 | Close the canvas and re-open the same file | File re-opens without error |
| 5 | Observe Preview mode | Updated JS output ("Updated") is shown |

## Expected Final State

The saved edit persists and the updated script output is visible after reopening the file.

## Pass/Fail Criteria

**Pass:**
- Reopened file's Preview mode shows the updated output

**Fail:**
- Reopened file shows the original (pre-edit) output, or the save fails
