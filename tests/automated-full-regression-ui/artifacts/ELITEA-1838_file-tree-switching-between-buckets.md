---
id: ELITEA-1838
title: "File Tree Behavior – Switching Between Buckets Updates Tree and Main Panel"
priority: high
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_tree_switch_between_buckets.TestArtifactsTreeSwitchBetweenBuckets.test_switching_buckets_updates_tree_and_main_panel
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1633
requirements: []
---

# ELITEA-1838: File Tree Behavior – Switching Between Buckets Updates Tree and Main Panel

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that switching between buckets updates the left panel tree selection, the main panel contents, and the URL correctly, and that the previously selected bucket does not collapse when another bucket is selected.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least two buckets exist: "bucket-1" (with files) and "bucket-2" (empty or with different files).

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket 1 | bucket-1 |
| Bucket 2 | bucket-2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify at least two buckets are present: "bucket-1" and "bucket-2" | Both buckets are visible |
| 3 | Click on "bucket-1" — verify it is highlighted, expands in the left panel tree and its files are shown in the main panel | "bucket-1" is highlighted, expanded, and files are shown |
| 4 | Click on "bucket-2" — verify "bucket-1" does NOT collapse but loses its highlighted state | "bucket-1" remains expanded but unhighlighted; "bucket-2" becomes highlighted |
| 5 | Verify "bucket-2" becomes highlighted and its contents (or empty state) are shown in the main panel | "bucket-2" is highlighted and main panel shows its contents |
| 6 | Verify the main panel header/breadcrumb updates to display "bucket-2" | Breadcrumb shows "bucket-2" |
| 7 | Verify the URL in the browser address bar updates to reflect "bucket-2" | URL reflects "bucket-2" |
| 8 | Click back on "bucket-1" — verify "bucket-1" becomes highlighted again and expanded | "bucket-1" is re-selected and highlighted |
| 9 | Verify the main panel displays "bucket-1" contents again | Main panel shows "bucket-1" files |

---

## Expected Final State

Switching between buckets updates the main panel content, breadcrumb, and URL correctly. "bucket-1" remains expanded (not collapsed) when "bucket-2" is selected.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Main panel, breadcrumb, and URL update on bucket switch; previous bucket stays expanded.

**Fail:**
- Any step produces an error or unexpected result.
- Main panel doesn't update, breadcrumb or URL is wrong, or previous bucket collapses.
