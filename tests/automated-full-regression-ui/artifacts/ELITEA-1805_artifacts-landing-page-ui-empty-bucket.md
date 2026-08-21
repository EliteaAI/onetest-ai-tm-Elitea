---
id: ELITEA-1805
title: "Artifacts Landing Page UI – Empty Bucket (No Files)"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_landing_page_ui.TestArtifactsLandingPageUI.test_landing_page_empty_bucket
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1625
requirements: []
---

# ELITEA-1805: Artifacts Landing Page UI – Empty Bucket (No Files)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Artifacts landing page renders the correct empty state UI when a bucket containing no files is selected, including the "No files in this bucket" message, upload button, and retention policy tooltip.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one empty bucket exists in the project (e.g. "as").

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name (empty) | as |
| Tooltip content | Retention Policy: X, Number of files: 0 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify the left panel header displays "BUCKETS" label with a folder icon and a search icon | Header is correctly displayed |
| 3 | Verify the list of buckets is displayed in the left panel under the storage provider with a dropdown arrow | Bucket list is visible |
| 4 | Click on a bucket that contains no files (e.g. "as") | Bucket is selected |
| 5 | Verify the selected bucket is highlighted in the left panel and the text "No files in this bucket" is displayed below the bucket name in the left panel tree | Bucket is highlighted and "No files in this bucket" text appears in left panel |
| 6 | Verify the bucket name is displayed as a header/title in the top of the main (right) panel | Main panel header shows the bucket name |
| 7 | Verify the main panel does not display a file table or any file rows | No file table is shown |
| 8 | Verify the main panel displays an empty state with an icon, the message "No files in this bucket" and an "Upload files" button in the center of the panel | Empty state with icon, message, and upload button is shown in the center |
| 9 | Verify the top-right of the main panel contains a Search bar and upload / download / delete icons | All top-right icons are present |
| 10 | Verify the bottom of the left panel displays "Buckets: N  Size: X MB" reflecting the actual number of buckets and total size | Footer shows correct bucket count and size |
| 11 | Hover over the bucket name in the left panel — verify a tooltip appears showing "Retention Policy: X" and "Number of files: 0" | Tooltip appears with correct retention policy and 0 file count |

---

## Expected Final State

The empty bucket state is rendered correctly: no file table is shown in the main panel, the center empty state message with "Upload files" button is displayed, and the tooltip on hover shows the correct retention policy and 0 file count.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Empty state message, upload button, and tooltip are all displayed correctly.

**Fail:**
- Any step produces an error or unexpected result.
- File table is shown when bucket is empty, or empty state elements are missing.
