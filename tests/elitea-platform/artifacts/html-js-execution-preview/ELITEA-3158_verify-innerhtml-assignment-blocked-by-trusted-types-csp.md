---
id: ELITEA-3158
title: "Verify innerHTML assignment with HTML strings is blocked by Trusted Types CSP"
priority: high
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
- Browser DevTools available to inspect Console output

> ⚠️ **Known behavior:** `innerHTML` with HTML strings is blocked by CSP — confirmed during bench-report testing. `createElement`/`textContent`/`appendChild` must be used instead.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `{{sharepoint_test_files_url}}` |
| File | `innerhtml-test.html` — compares `innerHTML = '<tag>...'` vs. `createElement`/`textContent` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `innerhtml-test.html` and open in Preview mode | Page renders both test results |
| 2 | Observe the `innerHTML` assignment test | Shows **BLOCKED** (content not rendered) |
| 3 | Observe the `createElement`/`textContent` equivalent test | Shows **PASS** (content rendered) |
| 4 | Open DevTools → Console | Trusted Types or CSP violation logged for the `innerHTML` attempt |

## Expected Final State

`innerHTML` with raw HTML strings remains blocked by Trusted Types CSP; the safe DOM-construction pattern continues to work.

## Pass/Fail Criteria

**Pass:**
- innerHTML attempt is BLOCKED with a Trusted Types/CSP violation; createElement equivalent PASSES

**Fail:**
- innerHTML assignment succeeds and renders raw HTML (Trusted Types bypass)
