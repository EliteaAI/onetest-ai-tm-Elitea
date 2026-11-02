---
id: ELITEA-3154
title: "Verify HTML file accessed from Chat canvas also supports inline JS"
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
- User has access to a Chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | HTML file with inline script, uploaded/generated in a Chat conversation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a Chat conversation, upload or generate an HTML file with an inline script | File appears as an attachment/artifact in chat |
| 2 | Click the eye/preview icon to open the file in canvas from Chat | Canvas opens with the file loaded |
| 3 | Observe Preview mode | JS output renders correctly |
| 4 | Switch to Raw mode | Source is shown correctly |

## Expected Final State

HTML files opened from Chat canvas behave identically to those opened from Artifacts for JS execution purposes.

## Pass/Fail Criteria

**Pass:**
- JS executes and renders in Preview mode when opened via Chat canvas

**Fail:**
- JS does not execute, or Preview mode is unavailable when opened via Chat canvas
