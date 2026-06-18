---
id: ELITEA-0265
title: "Folder Nodes Within an Expanded Bucket Expand and Collapse Independently"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [bug-area:not-current-release-scope, feat:artifacts, eng:frontend, bug-env:DEV, r-2.0.4, nfr:ui]
requirements: [EliteaAI/elitea_issues#5222]
---
# ELITEA-0265: Folder Nodes Within an Expanded Bucket Expand and Collapse Independently

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that individual folder nodes inside an expanded bucket tree can be expanded and collapsed independently without collapsing the parent bucket or affecting sibling folders.

**Coverage:**
- Folder click expands the folder revealing its contents
- Second click on same folder collapses it
- Parent bucket remains expanded when a child folder is collapsed
- Two folders can be simultaneously expanded
- Collapsing one folder does not collapse the other

## Preconditions

- Logged in to {{base_url}} (Private project)
- A bucket exists with at least two nested folders, each containing at least one file

## Test Data

- Bucket with nested folders (e.g., `test` or `regr`)
- Two distinct folder names within the bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts and click a bucket that contains folders | Bucket expands in the sidebar; folder nodes are visible |
| 2 | Click a folder node (Folder A) in the sidebar tree | Folder A expands, revealing its contents (files or sub-folders) |
| 3 | Click the same folder node (Folder A) again | Folder A collapses, hiding its contents; bucket itself remains expanded |
| 4 | Click a second folder node (Folder B) in the same bucket | Folder B expands independently |
| 5 | Click Folder A again to expand it | Folder A expands again; Folder B remains expanded |
| 6 | Click Folder A to collapse it | Folder A collapses; Folder B stays expanded; bucket stays expanded |

## Expected Final State

Folder A collapses; Folder B stays expanded; bucket stays expanded

## Pass/Fail Criteria

**Pass:**
- Each folder toggles independently on click
- Collapsing a folder does not collapse the parent bucket
- Multiple folders can be simultaneously expanded

**Fail:**
- Clicking a folder collapses the entire bucket
- Collapsing one folder collapses other folders
- Folder click has no effect
