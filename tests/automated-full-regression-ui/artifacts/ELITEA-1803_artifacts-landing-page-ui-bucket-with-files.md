---
id: ELITEA-1803
title: "Artifacts Landing Page UI – Bucket with Files (at least 1 file)"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1803: Artifacts Landing Page UI – Bucket with Files (at least 1 file)

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that the Artifacts landing page renders all expected UI elements correctly when a bucket containing at least one file is selected, including left panel header, bucket list, file table columns, pagination controls, and action icons.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one bucket exists in the project containing at least one file (e.g. "add-as-attachment" with "12.png").

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | add-as-attachment |
| File name | 12.png |
| File type | PNG Image |
| File size | 295.9 KB |
| Last update | 29-01-2026, 06:11 PM |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads and the left panel is displayed |
| 2 | Verify the left panel header displays "BUCKETS" label with a folder (create bucket) icon and a search (magnifier) icon next to it | Header shows "BUCKETS" with both icons present |
| 3 | Verify the list of buckets is displayed in the left panel under the storage provider (e.g. "Elitea S3 storage") with a dropdown arrow | Bucket list is visible under the storage provider with dropdown arrow |
| 4 | Click on a bucket that contains at least one file (e.g. "add-as-attachment") | Bucket is selected and expanded in the left panel |
| 5 | Verify the selected bucket is highlighted in the left panel and its file(s) are listed below the bucket name (e.g. "12.png") | Selected bucket is highlighted and files are listed beneath it |
| 6 | Verify the bucket name is displayed as a header/title in the top of the main (right) panel | Main panel header shows the bucket name |
| 7 | Verify the main panel displays a file table with columns: Name, Type, Size, Last update, Actions | File table is present with all five columns |
| 8 | Verify each file row contains a checkbox, file name, file type, file size, last-update timestamp and an actions icon | Each row shows checkbox, name, type (e.g. "PNG Image"), size (e.g. "295.9 KB"), timestamp (e.g. "29-01-2026, 06:11 PM") and actions icon |
| 9 | Verify the top-right of the main panel contains a Search bar and upload / download / delete icons | Search bar and upload, download, delete icons are all present in the top-right area |
| 10 | Verify the bottom of the left panel displays "Buckets: N  Size: X MB" reflecting the actual number of buckets and total size | Footer shows correct bucket count and total size |
| 11 | Verify the bottom of the main panel displays a "Rows per page" dropdown with a default value of 10 | "Rows per page" dropdown is present and defaults to 10 |
| 12 | Verify the pagination control displays the current range and total (e.g. "1 - 1 of 1") reflecting the actual number of files | Pagination shows correct range and total |
| 13 | Verify the pagination prev < and next > navigation arrows are present next to the page indicator | Both prev and next arrows are present |
| 14 | Verify the prev < arrow is disabled when on the first page | Prev arrow is disabled/greyed out on first page |
| 15 | Verify the next > arrow is disabled when all files fit on one page | Next arrow is disabled/greyed out when all files fit on one page |

---

## Expected Final State

All Artifacts landing page UI elements are rendered correctly for a bucket with files: bucket list is visible in left panel, file table with all columns and correct data is shown in the main panel, pagination and navigation controls are present and in correct states.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All UI elements (header, bucket list, file table, pagination, icons) are displayed correctly and in the expected state.

**Fail:**
- Any step produces an error or unexpected result.
- Any UI element is missing, incorrectly labelled, or in the wrong state.
