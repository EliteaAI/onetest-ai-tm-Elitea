---
id: ELITEA-0719
title: "Regression: Reindex of All-Valid Index Has No False Skips"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0719: Regression: Reindex of All-Valid Index Has No False Skips

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the skip logic does not incorrectly mark valid files as "skipped" during a reindex — document count must remain equal to the full valid file count with no unexpected skips.

**Coverage:**
- Reindex of all-valid index completes with ✅ Completed
- Document count matches total valid file count (no decrease)
- No unexpected "files skipped" messages in notifications or progress log

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index built from `all-valid-test` bucket

## Test Data

- Bucket: `all-valid-test` (5 valid files)
- Expected count after reindex: `5`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact Toolkit → Indexes Tab. Select the existing all-valid index. | Index selected. |
| 2 | Click Reindex. | Reindex starts. Status = 🔄 In Progress. |
| 3 | Wait for completion. Check the final status. | Status = ✅ Completed. |
| 4 | Read the document count from the sidebar card or History tab. | Count = 5 — matches total valid files, unchanged. |

## Expected Final State

Count = 5 — matches total valid files, unchanged.

## Pass/Fail Criteria

**Pass:**
- Status = ✅ Completed
- Document count = 5 (no false skips)
- No unexpected skip messages

**Fail:**
- Count drops below 5 (false skips of valid files)
- Skip messages appear despite all files being valid
