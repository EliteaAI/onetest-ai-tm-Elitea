---
id: ELITEA-2855
title: "Verify DOMContentLoaded fires reliably; scripts at bottom of <body> run without it"
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
| File | `domcontentloaded-test.html` — tests a direct call at bottom of body vs. a `DOMContentLoaded` listener |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `domcontentloaded-test.html` and open in Preview mode | Page renders both test results |
| 2 | Observe the "direct call at bottom of body" test | Shows **PASS** |
| 3 | Observe the "DOMContentLoaded listener" test | Record pass or fail — both are valid data points |
| 4 | Document the observed timing behavior | Result matches documented expected behavior for script authors |

## Expected Final State

The reliable pattern (direct call at bottom of body) is confirmed to work; `DOMContentLoaded` timing behavior is documented either way.

## Pass/Fail Criteria

**Pass:**
- Direct call at bottom of body test shows PASS

**Fail:**
- Direct call at bottom of body test fails (this is the reliable pattern; regression here is a defect)
