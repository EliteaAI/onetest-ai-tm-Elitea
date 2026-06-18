---
id: ELITEA-0275
title: "Pinned and unpinned buckets are visually distinguishable by pin icon state without a labeled section header"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0275: Pinned and unpinned buckets are visually distinguishable by pin icon state without a labeled section header

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that pinned and unpinned buckets are visually distinguished via pin icon state (filled vs. hover-only), consistent with the chat folder pinning design — without an explicit "Pinned Buckets" section header or separator.

**Coverage:**
- Filled 📌 icon is always visible on pinned buckets (not hover-dependent)
- Unpinned buckets show no icon by default; outline icon appears on hover only
- No "Pinned Buckets" section label or divider element is rendered between pinned and unpinned groups
- Visual ordering (pinned at top, unpinned below) is self-evident

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least 2 buckets pinned and at least 2 unpinned

## Test Data

- At least 2 pinned buckets and 2 unpinned buckets

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts with a mix of pinned (at least 2) and unpinned (at least 2) buckets visible in the sidebar. | Bucket sidebar shows pinned buckets at the top and unpinned below. |
| 2 | Observe pinned buckets without hovering over them. | Filled/solid 📌 pin icon is persistently visible on each pinned bucket row without any hover. |
| 3 | Observe unpinned buckets without hovering. | No pin icon is visible on unpinned bucket rows. |
| 4 | Hover over an unpinned bucket. | Outline/empty pin icon appears on that row. |
| 5 | Move cursor away from the unpinned bucket. | Outline pin icon disappears; row returns to default appearance. |
| 6 | Inspect the sidebar area between pinned and unpinned buckets for any section heading or divider. | No 'Pinned Buckets' label, header text, or visible separator bar is rendered between the two groups. |
| 7 | Verify the visual ordering of the bucket sidebar. | Pinned buckets are unambiguously at the top; unpinned buckets are below; ordering is clear without an explicit separator. |

## Expected Final State

Pinned buckets are unambiguously at the top; unpinned buckets are below; ordering is clear without an explicit separator.

## Pass/Fail Criteria

**Pass:**
- Filled icon persistently visible on pinned buckets without hover
- Outline icon hover-only on unpinned buckets; disappears when cursor moves away
- No explicit "Pinned Buckets" section header or separator is rendered
- Visual ordering (pinned at top, unpinned below) is clear

**Fail:**
- Icons are the same state for both pinned and unpinned groups
- Filled icon disappears on pinned bucket when cursor is not hovering
- Explicit "Pinned Buckets" label or separator bar is unexpectedly rendered
- Visual distinction between pinned and unpinned groups is absent
