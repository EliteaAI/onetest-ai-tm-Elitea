---
id: ELITEA-2854
title: "Verify defer and async attributes on <script> tags work correctly"
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
| File | `defer-async-test.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `defer-async-test.html` and open in Preview mode | Page renders both test results |
| 2 | Observe the `defer` script result | Shows PASS (script ran after DOM was ready) |
| 3 | Observe the `async` script result | Shows PASS (script ran at some point) |
| 4 | If either fails, check for side effects | Failure is graceful; other scripts are unaffected |

## Expected Final State

`defer`/`async` loading semantics are respected, or fail gracefully without breaking other scripts on the page.

## Pass/Fail Criteria

**Pass:**
- Both defer and async scripts execute successfully (or fail without breaking the page)

**Fail:**
- Either script breaks page execution or crashes the preview
