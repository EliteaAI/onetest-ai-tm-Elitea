---
id: ELITEA-1251
title: "Clean Index With No Path on Special-Character Libraries Re-indexes Correctly"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1251: Clean Index With No Path on Special-Character Libraries Re-indexes Correctly

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Clean Index flag works correctly when re-indexing a site without a path that contains special-character document library names — old index data is cleared and fresh data is indexed.

**Coverage:**
- Existing no-path index is re-run with Clean Index = true
- Re-indexing completes without error on a site with special-character library names
- Total indexed count reflects freshly indexed content (not stale or double-counted)
- Post-re-index search still returns correct results

## Preconditions

- A completed no-path index named `nopath` exists with a non-zero total indexed count (TC: index_data Without Path Succeeds on Site With Special-Character Document Library Names must have passed)

## Test Data

- Index Name: `clntest` (new clean index run)
- Clean Index: checked (true)
- Path: (empty)
- Search query post-re-index: same unique phrase used in the searchability test (e.g., "SharePoint retest content unique phrase")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → SharePoint toolkit → Indexes tab | Indexes tab is displayed |
| 2 | Click + (New Index); enter `clntest` as Index Name; check Clean Index; leave Path empty | Form shows `clntest` with Clean Index checked, Path blank |
| 3 | Click Index | Indexing job starts |
| 4 | Wait for the job to complete | Job completes without error |
| 5 | Check the total indexed counter for `clntest` | Counter reflects files from all libraries (non-zero); count is consistent with expected file count, not doubled |
| 6 | In the Run tab for `clntest`, use Search Index with the unique phrase | At least one result is returned correctly |

## Expected Final State

At least one result is returned correctly

## Pass/Fail Criteria

**Pass:**
- Re-indexing with Clean Index completes without error
- Total indexed count is consistent (not doubled or 0)
- Search returns correct results after clean re-index

**Fail:**
- "Index processing error" appears during re-index
- Total indexed count is 0 or unexpectedly doubled
- Search returns no results after clean re-index
