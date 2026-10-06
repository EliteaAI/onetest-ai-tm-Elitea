---
id: ELITEA-1804
title: "Artifacts Landing Page UI – Bucket with More Than 10 Files and Pagination"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1804: Artifacts Landing Page UI – Bucket with More Than 10 Files and Pagination

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Artifacts landing page pagination works correctly when a bucket contains more than 10 files, including correct display of rows, pagination counters, and prev/next arrow states.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket exists containing more than 10 files (e.g. 12 files). If not, upload the required number of files first.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket file count | 12 (or more than 10) |
| Rows per page default | 10 |
| First page range | 1 - 10 of 12 |
| Second page range | 11 - 12 of 12 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on a bucket that contains more than 10 files (e.g. a bucket with 12 files); if not, upload them | Bucket is selected and main panel shows its files |
| 3 | Verify the selected bucket is highlighted in the left panel and its files are listed in the main panel | Bucket is highlighted and file list is visible |
| 4 | Verify the main panel displays a file table with columns: Name, Type, Size, Last update, Actions | File table is present with all five columns |
| 5 | Verify the bottom of the main panel displays a "Rows per page" dropdown with a default value of 10 | Dropdown shows default value of 10 |
| 6 | Verify only 10 file rows are displayed in the file table on the first page | Exactly 10 rows are shown on the first page |
| 7 | Verify the pagination control displays the current range and total reflecting the first page (e.g. "1 - 10 of 12") | Pagination shows "1 - 10 of 12" |
| 8 | Verify the prev < arrow is disabled on the first page | Prev arrow is disabled |
| 9 | Verify the next > arrow is active/enabled | Next arrow is enabled |
| 10 | Click the next > arrow | Page navigates to the next set of files |
| 11 | Verify the page indicator updates to the next range (e.g. "11 - 12 of 12") | Pagination updates to "11 - 12 of 12" |
| 12 | Verify the prev < arrow becomes active/enabled after navigating away from the first page | Prev arrow is now enabled |
| 13 | Verify the file table updates and displays the next set of up to 10 files | File table shows the remaining files |
| 14 | Verify the next > arrow remains active if more pages exist, or becomes disabled if the last page is reached | Next arrow is disabled on the last page |
| 15 | Verify the next > arrow is disabled on the last page | Next arrow is disabled |
| 16 | Verify only the remaining files (e.g. 2 out of 12) are displayed in the file table on the last page | Only remaining files are shown |
| 17 | Click the prev < arrow | Page navigates back to the previous page |
| 18 | Verify the page indicator updates back to the previous range (e.g. "1 - 10 of 12") | Pagination updates back to "1 - 10 of 12" |
| 19 | Verify the prev < arrow is disabled again on the first page | Prev arrow is disabled again |
| 20 | Verify 10 file rows are displayed in the file table on the first page | Exactly 10 rows are shown again |

---

## Expected Final State

Pagination works correctly for buckets with more than 10 files: first page shows 10 rows with correct counter and disabled prev arrow, navigation to next page updates counter and enables prev arrow, last page disables next arrow, navigation back returns to correct state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pagination counters, row counts, and arrow states are correct on all pages.

**Fail:**
- Any step produces an error or unexpected result.
- Pagination counter is incorrect, wrong number of rows displayed, or arrow states are wrong.
