---
id: ELITEA-3163
title: "Verify infinite loop in inline JS freezes only the preview tab, not ELITEA"
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
- Test performed in an isolated browser tab; be prepared to force-kill the tab

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `infinite-loop.html` — contains `while(true){}` in an inline script |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `infinite-loop.html` and open in Preview mode | Browser tab becomes unresponsive |
| 2 | Close the canvas modal or navigate away (force-kill tab if needed) | Tab can be closed/reloaded |
| 3 | Reload ELITEA | ELITEA is fully operational, no data loss |
| 4 | Check other open ELITEA tabs (if any) | Other tabs are unaffected |

## Expected Final State

The infinite loop's impact is contained to the single browser tab hosting the preview; ELITEA application state is unaffected.

## Pass/Fail Criteria

**Pass:**
- Only the affected tab freezes; ELITEA recovers fully on reload with no data loss

**Fail:**
- ELITEA state is corrupted, other tabs/users are affected, or data loss occurs
