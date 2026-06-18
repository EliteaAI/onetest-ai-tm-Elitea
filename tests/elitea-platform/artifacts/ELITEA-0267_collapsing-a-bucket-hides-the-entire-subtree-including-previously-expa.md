---
id: ELITEA-0267
title: "Collapsing a Bucket Hides the Entire Subtree Including Previously Expanded Folders"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [bug-area:not-current-release-scope, feat:artifacts, eng:frontend, bug-env:DEV, r-2.0.4, nfr:ui]
requirements: [EliteaAI/elitea_issues#5222]
---
# ELITEA-0267: Collapsing a Bucket Hides the Entire Subtree Including Previously Expanded Folders

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that collapsing a bucket hides the entire subtree — including any previously expanded nested folders — leaving no partial tree visible in the sidebar.

**Coverage:**
- Nested folder expanded before bucket collapse
- Entire subtree (bucket tree + expanded folder contents) hides on bucket collapse
- No partial subtree or orphan items remain visible after collapse

## Preconditions

- Logged in to {{base_url}} (Private project)
- A bucket exists with at least one nested folder containing files

## Test Data

- Bucket with nested folder (e.g., `regr` or `test`)
- A named subfolder within that bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts and click a bucket that contains nested folders | Bucket expands; folder nodes are visible in the sidebar tree |
| 2 | Click a nested folder node to expand it | Folder opens, showing its files or sub-folders in the tree |
| 3 | Click the bucket name to collapse the bucket | The entire subtree disappears — both the bucket's direct items AND the previously expanded folder's contents are hidden; no partial tree remains |
| 4 | Inspect the sidebar for any orphan items beneath the collapsed bucket | No residual items (files, folder names, sub-nodes) are visible beneath the collapsed bucket |

## Expected Final State

No residual items (files, folder names, sub-nodes) are visible beneath the collapsed bucket

## Pass/Fail Criteria

**Pass:**
- Entire subtree including expanded folder contents is hidden after bucket collapse
- No orphan nodes remain in the sidebar

**Fail:**
- Previously expanded folder's contents remain partially visible after bucket collapse
- Any child items remain visible under a collapsed bucket
