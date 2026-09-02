---
id: ELITEA-2872
title: "Verify .txt file is plain text (no Preview/JS) until language dropdown is switched to HTML"
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `inline-script-basic.txt` — identical content to `inline-script-basic.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `inline-script-basic.txt` and open the file | File is recognized as plain text — no Preview tab/mode is available, inline script does not execute |
| 2 | Locate the language dropdown and change it to "HTML" | Preview mode becomes available |
| 3 | Open Preview mode | Text "JS ran" is visible, confirming the inline script executed |
| 4 | Check for error banners | No error banner is shown at any step |

## Expected Final State

JS execution and Preview mode are gated by the resolved language, not merely the file extension.

## Pass/Fail Criteria

**Pass:**
- `.txt` shows no Preview/JS by default; switching language to HTML enables both

**Fail:**
- `.txt` file executes JS without a language override, or switching to HTML fails to enable Preview
