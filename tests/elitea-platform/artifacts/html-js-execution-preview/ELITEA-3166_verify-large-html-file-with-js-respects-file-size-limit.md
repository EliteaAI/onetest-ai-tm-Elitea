---
id: ELITEA-3166
title: "Verify large HTML file with inline JS respects the file size limit for preview"
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
| File | `large-html-with-js.html` — file size > 2 MB, contains an inline script |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `large-html-with-js.html` | Upload succeeds |
| 2 | Attempt to open the file in preview | Appropriate error message is displayed (e.g., "File too large for preview") |
| 3 | Confirm application stability | No crash or broken canvas |

## Expected Final State

The existing 2 MB preview size limit continues to apply consistently to JS-containing HTML files.

## Pass/Fail Criteria

**Pass:**
- A clear size-limit error is shown; no crash

**Fail:**
- Preview attempts to render anyway and crashes, or no error is shown at all
