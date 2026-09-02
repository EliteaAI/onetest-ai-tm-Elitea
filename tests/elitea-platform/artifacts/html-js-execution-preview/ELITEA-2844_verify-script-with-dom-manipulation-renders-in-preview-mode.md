---
id: ELITEA-2844
title: "Verify <script> with DOM manipulation renders correctly in Preview mode"
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
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `dom-manipulation.html` — inline script creates a list of items on `DOMContentLoaded` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `dom-manipulation.html` and open in Preview mode | Dynamically created list is rendered |
| 2 | Switch to Raw mode | Source code is shown, not rendered output |
| 3 | Switch back to Preview mode | Rendered output reappears correctly |

## Expected Final State

The dynamically generated DOM content renders correctly and consistently across Preview/Raw toggling.

## Pass/Fail Criteria

**Pass:**
- Dynamic list renders in Preview; Raw shows source; switching back re-renders correctly

**Fail:**
- Dynamic list fails to render, or content is lost/incorrect after toggling modes
