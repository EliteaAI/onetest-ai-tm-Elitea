---
id: ELITEA-3174
title: "Verify clicking inside the preview frame does not permanently steal keyboard focus"
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
- Any HTML file exists in an artifact bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | Any HTML file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the file in Preview mode | Preview renders |
| 2 | Click inside the preview frame | Focus moves into the iframe |
| 3 | Without clicking outside the canvas, use an ELITEA keyboard shortcut or click a navigation element | ELITEA responds normally |

## Expected Final State

Focus can move freely between the preview iframe and the rest of the ELITEA UI without a "dead" input state.

## Pass/Fail Criteria

**Pass:**
- ELITEA UI remains responsive to keyboard/navigation input after interacting with the preview

**Fail:**
- ELITEA UI becomes unresponsive to keyboard input until the page is reloaded
