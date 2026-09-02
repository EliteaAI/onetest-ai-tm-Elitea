---
id: ELITEA-2875
title: "Verify submitting a <form> inside the preview iframe does not navigate away from the preview"
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
- Browser DevTools available to inspect navigation behavior

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `form-submit-test.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `form-submit-test.html` and open in Preview mode | Form renders |
| 2 | Click the **Submit** button | Submission attempt occurs |
| 3 | Wait ~2 seconds and read the Verdict line | Shows `PASS — submit event fired but no navigation occurred` OR `PASS — sandbox blocked form submission entirely before the submit event could fire` |
| 4 | If Verdict shows `NAVIGATED`, check DevTools | Only the iframe navigated, not the ELITEA parent page/URL bar |
| 5 | Confirm the ELITEA address bar | Never changes regardless of which verdict is shown |

## Expected Final State

Form submission inside the sandboxed preview iframe never affects the ELITEA parent page or its URL.

## Pass/Fail Criteria

**Pass:**
- Address bar never changes; verdict is one of the two healthy outcomes

**Fail:**
- The ELITEA parent page navigates or its address bar changes as a result of the form submission
