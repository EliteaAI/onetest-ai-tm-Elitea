---
id: ELITEA-3176
title: "Verify window.innerWidth/innerHeight returns iframe dimensions, not parent page dimensions"
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
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | `canvas-resize-test.html` — displays `window.innerWidth`/`window.innerHeight` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `canvas-resize-test.html` and open in Preview mode at default canvas size | Reported dimensions are shown |
| 2 | Note the reported dimensions | Values reflect the iframe's viewport, not the full browser window |
| 3 | Resize the canvas (if resizable) | Reported dimensions update to match the iframe size |

## Expected Final State

Responsive layout logic relying on `window.innerWidth`/`innerHeight` receives the iframe's own dimensions.

## Pass/Fail Criteria

**Pass:**
- Reported dimensions match the iframe viewport and update on resize

**Fail:**
- Reported dimensions match the full browser window instead of the iframe
