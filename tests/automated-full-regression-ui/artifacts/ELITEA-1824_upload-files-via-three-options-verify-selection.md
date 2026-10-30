---
id: ELITEA-1824
title: "Upload Flow: Three upload paths, subfolder/root destinations, nested paths"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1824: Upload Flow: Three upload paths, subfolder/root destinations, nested paths

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify all three upload entry points work correctly, that files can be uploaded to subfolders and bucket root, that nested non-existing folder paths are auto-created, and that breadcrumbs and URLs update appropriately.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists and is empty.
- Test files available: sample.txt, sample.png, sample.md, sample2.txt

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder (existing) | a1 |
| Nested subfolder (non-existing) | a1/nested/deep |
| Upload file 1 | sample.txt |
| Upload file 2 | sample.png |
| Upload file 3 | sample.md |
| Upload file 4 | sample2.txt |

---

## Steps

### Part 1: Center Button Upload to Subfolder

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts section | Artifacts page loads |
| 2 | Click on "bucket-1" in bucket list | Bucket selected; main panel shows empty state with "Upload files" button |
| 3 | Click center "Upload files" button | System file explorer opens |
| 4 | Select "sample.txt" and click Open | "Upload files to..." modal opens with Path: "bucket-1" |
| 5 | Append "/a1" to path so it reads "bucket-1/a1" | Path field shows "bucket-1/a1" |
| 6 | Click Upload | Upload completes; success notification appears |
| 7 | Verify subfolder "a1" appears under "bucket-1" in left panel | Subfolder "a1" is visible |
| 8 | Verify breadcrumb shows "bucket-1 > a1" | Breadcrumb is correct |
| 9 | Verify "sample.txt" is listed in file table with metadata | File is present with Name, Type, Size, Last update |

### Part 2: Top-Right Icon Upload to Same Subfolder

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Click upload icon in top-right corner of main panel | System file explorer opens |
| 11 | Select "sample.png" and click Open | "Upload files to..." modal opens with Path: "bucket-1/a1" (pre-filled) |
| 12 | Verify path is pre-filled with "bucket-1/a1" | Path shows current location |
| 13 | Click Upload | Upload completes; success notification appears |
| 14 | Verify "sample.png" is listed alongside "sample.txt" in file table | Both files visible in "bucket-1 > a1" |

### Part 3: Bucket 3-Dot Menu Upload to Root

| # | Action | Expected Result |
|---|--------|-----------------|
| 15 | In left panel, hover over "bucket-1" and click 3-dot menu | Dropdown menu appears with options |
| 16 | Verify dropdown shows: Upload files, Pin to top, Edit, Delete | All options visible |
| 17 | Click "Upload files" | System file explorer opens |
| 18 | Select "sample.md" and click Open | "Upload files to..." modal opens with Path: "bucket-1" (root only) |
| 19 | Verify path shows "bucket-1" without subfolder | Path is "bucket-1" |
| 20 | Click Upload | Upload completes; success notification appears |
| 21 | Click "bucket-1" (root) in left panel | Root level view loads |
| 22 | Verify breadcrumb shows "bucket-1" | Breadcrumb at root level |
| 23 | Verify "sample.md" is listed at root level | File at root, not in subfolder |
| 24 | Click "a1" subfolder in left panel | Subfolder view loads |
| 25 | Verify "sample.txt" and "sample.png" are in subfolder; "sample.md" is NOT | Subfolder contains only 2 files |

### Part 4: Nested Non-Existing Folder Auto-Creation

| # | Action | Expected Result |
|---|--------|-----------------|
| 26 | Click upload icon in top-right | System file explorer opens |
| 27 | Select "sample2.txt" and click Open | "Upload files to..." modal opens |
| 28 | Change path to "bucket-1/a1/nested/deep" (non-existing nested path) | Path field shows nested path |
| 29 | Click Upload | Upload completes; success notification appears |
| 30 | In left panel, expand "bucket-1" → "a1" → "nested" | Nested folder structure is auto-created |
| 31 | Verify "nested" subfolder appears under "a1", and "deep" subfolder under "nested" | Full nested path exists |
| 32 | Click "deep" subfolder in left panel | Deep folder view loads |
| 33 | Verify breadcrumb shows "bucket-1 > a1 > nested > deep" | Breadcrumb shows full path |
| 34 | Verify "sample2.txt" is listed in "deep" folder | File in correct nested location |

### Part 5: URL Verification

| # | Action | Expected Result |
|---|--------|-----------------|
| 35 | Navigate between bucket root, "a1", and "deep" folders | Navigation works smoothly |
| 36 | Verify URL in browser address bar updates with bucket and folder parameters | URL reflects current path selection |

---

## Expected Final State

- All three upload entry points function correctly
- Files uploaded to subfolder "a1": sample.txt, sample.png
- File uploaded to bucket root: sample.md
- Nested path "a1/nested/deep" auto-created with sample2.txt
- Breadcrumbs and URLs update correctly for all navigation

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All upload paths work; files appear in correct locations; nested folders auto-created; breadcrumbs/URLs accurate.

**Fail:**
- Any upload option fails, files in wrong locations, nested path not created, or breadcrumb/URL incorrect.

---

## Notes

**Source functional tests:** ELITEA-1824, ELITEA-1827, ELITEA-1834, ELITEA-1835

**Regression rationale:** Consolidates all upload path variations into a comprehensive end-to-end flow covering the three upload entry points, subfolder vs root targeting, and nested path auto-creation.

**Selected checkpoints:**
- Center button upload (ELITEA-1824, ELITEA-1834)
- Top-right icon upload with pre-filled path (ELITEA-1824, ELITEA-1834)
- Bucket 3-dot menu upload to root (ELITEA-1824, ELITEA-1835)
- Nested non-existing folder auto-creation (ELITEA-1827)
- Breadcrumb and URL updates (ELITEA-1824)
