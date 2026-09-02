---
id: ELITEA-2857
title: "Verify document.write() works or fails gracefully in the preview iframe"
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
| File | `document-write-test.html` — calls `document.write('Hello from document.write')` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `document-write-test.html` and open in Preview mode | Page loads |
| 2 | Observe the rendered output | Either the inline text renders, or a clear error/no-op occurs |
| 3 | If the document is replaced entirely | Result is still visible and the preview does not crash |
| 4 | Record the observed behavior | Behavior matches documented expectation for script authors |

## Expected Final State

`document.write()` either renders content correctly or fails without crashing the preview frame.

## Pass/Fail Criteria

**Pass:**
- Content renders correctly, or fails without crashing the canvas

**Fail:**
- Preview frame crashes, freezes, or becomes unusable after the call
