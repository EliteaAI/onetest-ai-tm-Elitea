---
id: ELITEA-0268
title: "Expanding a Second Bucket While One Is Already Expanded"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [bug-area:not-current-release-scope, feat:artifacts, eng:frontend, bug-env:DEV, r-2.0.4, nfr:ui]
requirements: [EliteaAI/elitea_issues#5222]
---
# ELITEA-0268: Expanding a Second Bucket While One Is Already Expanded

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking a second bucket while the first is already expanded correctly expands the new bucket, updates the file table, and that the collapse toggle also works on the newly selected bucket.

**Coverage:**
- Clicking a non-selected bucket expands it and updates the file table
- Second bucket becomes the selected/active bucket
- Collapse toggle works correctly on the newly selected bucket
- No duplicate tree items or visual glitches in the sidebar

## Preconditions

- Logged in to {{base_url}} (Private project)
- At least 2 buckets exist (e.g., `test`, `cl-bucket`)

## Test Data

- Bucket A: `test`
- Bucket B: `cl-bucket`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts and click `test` | `test` expands in the sidebar; file table shows `test` contents |
| 2 | Click `cl-bucket` (a different, currently not expanded bucket) | `cl-bucket` expands in the sidebar; file table updates to show `cl-bucket` contents |
| 3 | Inspect the sidebar | No duplicate tree items; no visual glitches |
| 4 | Click `cl-bucket` again (already selected and expanded) | `cl-bucket` tree collapses; file table still shows `cl-bucket` contents |
| 5 | Verify `test` still appears in the sidebar without anomalies | `test` bucket row is visible and stable; no side effects from switching buckets |

## Expected Final State

`test` bucket row is visible and stable; no side effects from switching buckets

## Pass/Fail Criteria

**Pass:**
- Second bucket expands and becomes active on click
- Collapse toggle works on newly selected bucket
- No duplicate elements or visual glitches

**Fail:**
- Clicking the second bucket does not expand it
- Sidebar shows duplicate or corrupted tree entries
- Collapse toggle does not work on the newly selected bucket
