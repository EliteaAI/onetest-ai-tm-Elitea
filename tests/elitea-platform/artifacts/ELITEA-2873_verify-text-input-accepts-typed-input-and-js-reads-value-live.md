---
id: ELITEA-2873
title: "Verify <input type=text> accepts typed input and JS reads the value live"
priority: medium
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
| File | `text-input-basic.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `text-input-basic.html` and open in Preview mode | Text input renders |
| 2 | Click into the text field and type a short string | Field accepts focus and keyboard input |
| 3 | Observe the "Mirror:" line | Updates live to match what was typed |
| 4 | Observe the result line | Shows **PASS — input event fired, value = "..."** with the correct value |
| 5 | Check for error banners | No error banner is shown |

## Expected Final State

Plain text inputs are fully interactive inside the sandboxed preview, with `input` events reporting the correct live value.

## Pass/Fail Criteria

**Pass:**
- Mirror line and result line reflect the typed value in real time

**Fail:**
- Input field does not accept focus/typing, or the input event never fires
