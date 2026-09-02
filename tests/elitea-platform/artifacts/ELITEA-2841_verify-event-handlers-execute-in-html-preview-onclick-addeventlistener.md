---
id: ELITEA-2841
title: "Verify event handlers execute in HTML Preview mode (addEventListener and onclick)"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176, EliteaAI/elitea_issues#6494]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `js-diagnostic.html` — contains 4 diagnostic tests including Test 3 (`onclick` attribute) and Test 4 (`addEventListener`) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `js-diagnostic.html` to a bucket | File uploads successfully |
| 2 | Open the file in Preview mode | Diagnostic page renders with 4 test rows |
| 3 | Click the Test 4 button (addEventListener) | Test 4 row shows **PASS** |
| 4 | Click the Test 3 button (`onclick` attribute) | Test 3 row shows **PASS** |
| 5 | Check for error banners | No error banner is displayed |

## Expected Final State

Both `addEventListener`-based and `onclick`-attribute-based event handlers fire correctly and both diagnostic rows show PASS.

## Pass/Fail Criteria

**Pass:**
- Test 4 (addEventListener) shows PASS
- Test 3 (onclick attribute) shows PASS

**Fail:**
- Either test row shows FAIL after clicking its button (Test 3 currently fails due to open bug #6494 — expected to be resolved before this fix ships)
