---
id: ELITEA-2840
title: "Verify inline <script> executes successfully in HTML Preview mode"
priority: critical
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
| File (variant 1) | `inline-script-basic.html` — contains `<script>document.getElementById('out').textContent = 'JS ran';</script>` |
| File (variant 2) | `inline-script-basic.htm` — identical content, `.htm` extension |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `inline-script-basic.html` to the artifact bucket | File uploads successfully and appears in the bucket tree |
| 2 | Open the file via the eye icon or bucket tree click | File opens in canvas with **Preview** mode active by default |
| 3 | Observe the rendered output | Text "JS ran" is visible in the rendered output |
| 4 | Check for error banners | No error banner or JS-blocked warning is displayed |
| 5 | Repeat steps 1–4 using `inline-script-basic.htm` | Identical behavior — "JS ran" is visible, no error banner |

## Expected Final State

Both `.html` and `.htm` files render their inline script output ("JS ran") in Preview mode with no errors.

## Pass/Fail Criteria

**Pass:**
- "JS ran" text is visible in Preview mode for both `.html` and `.htm` variants
- No error banner or blocked-JS warning shown

**Fail:**
- "JS ran" text is missing or the script does not execute for either file variant
- An error banner or blocked-JS warning is shown despite the script being safe inline JS
