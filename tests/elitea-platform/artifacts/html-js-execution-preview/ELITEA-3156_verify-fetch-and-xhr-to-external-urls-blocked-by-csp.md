---
id: ELITEA-3156
title: "Verify fetch() and XMLHttpRequest to external URLs are blocked by CSP"
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
- Browser DevTools available to inspect Console and Network tabs

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `fetch-test.html` — attempts `fetch('https://httpbin.org/get')` and an `XMLHttpRequest` to the same host |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `fetch-test.html` and open in Preview mode | Page renders test results |
| 2 | Observe the `fetch()` result | Shows **BLOCKED** (network error or CSP violation) |
| 3 | Observe the `XMLHttpRequest` result | Shows **BLOCKED** |
| 4 | Open DevTools → Console | CSP or network errors are logged, no successful HTTP responses |

## Expected Final State

Outbound network requests from inline JS remain blocked despite JS execution being enabled.

## Pass/Fail Criteria

**Pass:**
- Both fetch and XHR attempts are blocked, confirmed in Console

**Fail:**
- Either request succeeds and returns real response data
