---
id: ELITEA-3155
title: "Verify setTimeout and setInterval fire correctly in the preview iframe"
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
| File | `timers-test.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `timers-test.html` and open in Preview mode | Page renders with timer test labels |
| 2 | Wait ~1 second | `setTimeout` label changes from "waiting" to "PASS — setTimeout fired" |
| 3 | Observe the `setInterval` counter for at least 3 seconds | Counter increments every second for at least 3 ticks |
| 4 | Check for error banners | No error banner is shown |

## Expected Final State

Both timer-based async APIs fire reliably inside the sandboxed preview.

## Pass/Fail Criteria

**Pass:**
- setTimeout fires once after ~1s; setInterval increments repeatedly

**Fail:**
- Either timer never fires, or an error banner appears
