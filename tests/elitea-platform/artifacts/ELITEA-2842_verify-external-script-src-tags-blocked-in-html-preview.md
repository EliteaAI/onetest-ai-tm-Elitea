---
id: ELITEA-2842
title: "Verify external <script src> tags are blocked from loading in HTML Preview mode"
priority: critical
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `external-script.html` — contains `<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>` plus dependent DOM manipulation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `external-script.html` to a bucket | File uploads successfully |
| 2 | Open the file in Preview mode | Canvas opens in Preview mode |
| 3 | Observe the JS-dependent content | Content that depends on the external script does NOT render |
| 4 | Open DevTools → Console | A CSP or sandbox violation error appears, not a JS runtime error |
| 5 | Review rendered output | No unexpected content from the external script is shown |

## Expected Final State

The remote script never loads or executes; the sandbox/CSP blocks it while inline JS elsewhere in the platform continues to work normally.

## Pass/Fail Criteria

**Pass:**
- External script fails to load, and dependent content does not render
- Console shows a CSP/sandbox block, not a runtime error

**Fail:**
- The external script loads and its dependent content renders
- No block indication appears in Console
