---
id: ELITEA-2322
title: "MDX File Listing in Artifacts Folder View"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2322: MDX File Listing in Artifacts Folder View

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify MDX files appear correctly in Artifacts folder listing

## Preconditions

- MDX files exist in Artifacts bucket

## Test Data

- Files: `test_file_1_under_1mb.mdx`, `2.mdx`, `3.mdx`, `sample-made-up-content.mdx`
- Bucket: `Elitea S3 storage`
- Folder: `mdx`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts section | Artifacts page opens |
| 2 | Select "Elitea S3 storage" bucket | Bucket expands |
| 3 | Navigate to "mdx" folder | Folder contents display |
| 4 | Observe the file listing | Files are listed |

## Expected Results

- MDX files are listed in the folder
- File type column shows "MDX"
- File size is displayed correctly
- Last update timestamp is shown
- Files are sortable by name, type, size, date
- "View/Edit file" action button is visible on each file

## Pass/Fail Criteria

**Pass:**
- All MDX files appear in listing
- Metadata (type, size, date) is correct
- Sorting and actions work properly

**Fail:**
- MDX files missing from listing
- Incorrect metadata
- Sorting or actions don't work
