---
id: ELITEA-1839
title: "Download Flow – Download Single File via Actions Dropdown"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1839: Download Flow – Download Single File via Actions Dropdown

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that a single file can be downloaded via the file row actions dropdown, that it downloads immediately without ZIP packaging, and that the downloaded file is accessible and not corrupted.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" exists and contains "sample.txt".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| File to download | sample.txt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" and navigate to subfolder "a1" | Subfolder "a1" is selected |
| 3 | Verify the file table displays files including "sample.txt" | "sample.txt" is visible in the table |
| 4 | Hover over the file row "sample.txt" and click the 3-dot (ellipsis) / actions icon on that row | Dropdown menu appears |
| 5 | Verify a dropdown menu appears with options: "Download" and "Delete" | Both options are visible |
| 6 | Click "Download" | File download initiates |
| 7 | Verify the file "sample.txt" starts downloading immediately to the local machine (no zip packaging) | Download starts immediately without ZIP preparation dialog |
| 8 | Verify the downloaded file name matches "sample.txt" | Downloaded file is named "sample.txt" |
| 9 | Verify the file is accessible and not corrupted after download | File can be opened and content is intact |
| 10 | Verify no progress modal or zip preparation dialog is shown for a single file download | No progress modal appears |

---

## Expected Final State

"sample.txt" downloads immediately via the actions dropdown without any ZIP preparation. The downloaded file is accessible and not corrupted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File downloads immediately; no ZIP dialog; downloaded file is accessible.

**Fail:**
- Any step produces an error or unexpected result.
- Download fails, file is corrupted, or ZIP preparation dialog appears for single file.
