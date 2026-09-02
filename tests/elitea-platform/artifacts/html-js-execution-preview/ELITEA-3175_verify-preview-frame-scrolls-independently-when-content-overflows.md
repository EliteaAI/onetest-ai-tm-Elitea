---
id: ELITEA-3175
title: "Verify preview frame scrolls independently when content overflows"
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
| File | `bench-report.html` — 12-row table with filters |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `bench-report.html` and open in Preview mode in a small canvas window | Content overflows the visible area |
| 2 | Observe the preview frame | Frame shows its own scrollbar |
| 3 | Scroll within the preview | ELITEA's outer page does not scroll instead |

## Expected Final State

Overflowing preview content scrolls within its own iframe, independent of the ELITEA page.

## Pass/Fail Criteria

**Pass:**
- Preview frame scrolls independently; outer page stays fixed

**Fail:**
- Scrolling the preview also scrolls the outer ELITEA page, or content is clipped with no scrollbar
