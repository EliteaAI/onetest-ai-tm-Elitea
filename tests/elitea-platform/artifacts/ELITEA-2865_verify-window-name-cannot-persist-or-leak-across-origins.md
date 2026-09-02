---
id: ELITEA-2865
title: "Verify window.name cannot persist or leak data across origin boundaries"
priority: medium
type: regression
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
| File | `window-name-test.html` — writes and reads back a `window.name` value |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `window-name-test.html` and open in Preview mode | Script writes and reads `window.name` |
| 2 | Observe the same-session read-back | Value is readable within the same iframe session |
| 3 | Close and reopen the preview | `window.name` is empty/reset — not persisted |

## Expected Final State

`window.name` behaves as an isolated, non-persistent value scoped to the current iframe session only.

## Pass/Fail Criteria

**Pass:**
- Value is readable within the same session but not persisted across reopen

**Fail:**
- Value persists across a fresh preview session, indicating a cross-boundary leak
