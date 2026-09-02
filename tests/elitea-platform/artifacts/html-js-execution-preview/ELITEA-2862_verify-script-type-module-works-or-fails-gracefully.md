---
id: ELITEA-2862
title: "Verify <script type=module> inline module scripts work or fail gracefully"
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
- An artifact bucket exists and is available for file upload
- Browser DevTools available to inspect Console output

> ℹ️ `module-script.html` imports a non-existent module (`./mod.js`); the page computes a `Verdict:` line from two independent signals — whether the module body ran at all, and whether a `window` `error` event fired.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `module-script.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `module-script.html` and open in Preview mode | Page loads |
| 2 | Wait ~1.5s for the on-page verdict to resolve | Verdict line resolves |
| 3 | Read the Verdict line | Shows `PASS — import failed, and a clear error surfaced` (expected/healthy) |
| 4 | Cross-check the `window 'error' event` line against DevTools Console | A fired event corresponds to a visible module-load error in Console |
| 5 | Confirm no unhandled exception breaks the rest of the frame | Preview remains stable regardless of verdict |

## Expected Final State

A failed module import surfaces a visible, non-silent error without breaking the rest of the preview frame.

## Pass/Fail Criteria

**Pass:**
- Verdict shows `PASS — import failed, and a clear error surfaced`

**Fail:**
- Verdict shows `FAIL — import failed with no error signal at all (silent failure)` or `UNEXPECTED — module ran despite missing import target`
