---
id: ELITEA-3173
title: "Verify right-click context menu inside preview does not expose raw HTML via View Page Source"
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
- Any HTML file exists in an artifact bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | Any HTML file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the file in Preview mode | Preview renders |
| 2 | Right-click inside the preview frame | Browser context menu appears |
| 3 | If "View Page Source" is present, click it | Note whether it shows the ELITEA app source or the iframe's own HTML |
| 4 | Record result | Documented as a security observation |

## Expected Final State

Context menu behavior inside the preview frame does not expose the ELITEA parent application's source.

## Pass/Fail Criteria

**Pass:**
- "View Page Source" (if present) shows only the iframe's own HTML, not ELITEA's app source

**Fail:**
- "View Page Source" exposes ELITEA application source code
