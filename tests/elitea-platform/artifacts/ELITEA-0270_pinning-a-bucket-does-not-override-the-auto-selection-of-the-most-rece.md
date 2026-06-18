---
id: ELITEA-0270
title: "Pinning a bucket does not override the auto-selection of the most recently active bucket on return"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0270: Pinning a bucket does not override the auto-selection of the most recently active bucket on return

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the existing auto-selection behavior (most recently active bucket is selected when returning to Artifacts) still works correctly when pinned buckets are present — the system should not default to the pinned bucket over the most recently used one.

**Coverage:**
- Auto-selection defaults to most recently active bucket, not the pinned one
- Pinned bucket at the top is not incorrectly treated as "selected" on page load
- Navigating away and back does not change the auto-selection to the pinned bucket
- Pinned bucket remains pinned in its position regardless of auto-selection behavior

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least 2 buckets available
- Bucket `a` is pinned but has not had recent file activity
- Bucket `bucket-for-agent1` is unpinned

## Test Data

- Pinned (inactive) bucket: `a`
- Active bucket: `bucket-for-agent1` (upload a file to make it most recently active)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible. |
| 2 | Pin bucket `a` via ⋮ → 'Pin to top' (ensure it has no recent file activity). | `a` is pinned at the top but has no recent file activity. |
| 3 | Click on the unpinned bucket `bucket-for-agent1`. | File list for `bucket-for-agent1` opens. |
| 4 | Upload any small file to `bucket-for-agent1`. | File uploads successfully; `bucket-for-agent1` becomes the most recently active bucket. |
| 5 | Navigate away from Artifacts (e.g., click 'Agents' in the sidebar). | Agents page opens. |
| 6 | Navigate back to Artifacts (click 'Artifacts' in the sidebar). | Artifacts page loads. |
| 7 | Observe which bucket is auto-selected/highlighted. | `bucket-for-agent1` (most recently active) is auto-selected, NOT the pinned `a` bucket. |
| 8 | Verify `a` remains pinned at the top with 📌 icon. | `a` is still pinned; only the selection highlight is on `bucket-for-agent1`. |

## Expected Final State

`a` is still pinned; only the selection highlight is on `bucket-for-agent1`.

## Pass/Fail Criteria

**Pass:**
- Most recently active bucket (`bucket-for-agent1`) is auto-selected on return
- Pinned bucket (`a`) remains pinned at the top but is not auto-selected

**Fail:**
- Pinned bucket is auto-selected instead of the most recently active bucket
- Auto-selection behavior is broken by the presence of pinned buckets
- No bucket is auto-selected (blank state)
