---
id: ELITEA-2866
title: "Verify history.pushState cannot change the browser URL bar from within the iframe"
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
- Browser DevTools available to inspect Console output

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `history-pushstate-test.html` — calls `history.pushState({}, '', '/injected-path')` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `history-pushstate-test.html` and open in Preview mode | Script runs on load |
| 2 | Observe the browser address bar | URL does not change |
| 3 | Open DevTools → Console | A SecurityError or blocked-operation message appears |

## Expected Final State

The ELITEA browser URL remains unaffected by JS running inside the sandboxed preview iframe.

## Pass/Fail Criteria

**Pass:**
- Address bar URL is unchanged; Console shows a block/SecurityError

**Fail:**
- Address bar URL changes to reflect the injected path
