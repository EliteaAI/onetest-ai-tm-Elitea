---
id: ELITEA-0720
title: "Search Returns Valid File Content Only After Partial Indexing — No Parsing Errors or Content Bleed"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0720: Search Returns Valid File Content Only After Partial Indexing — No Parsing Errors or Content Bleed

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that `search_index` returns results only from successfully indexed files after a partial run — no parsing error entries and no content from corrupted or unsupported files in the output.

**Coverage:**
- `search_index` returns relevant results from valid file content
- No "Error during content parsing for file" entries appear in results
- No content from corrupted, unsupported, or password-protected files bleeds into results

## Preconditions

- Logged in to {{base_url}}
- Partial indexing completed on `mixed-files-test` (3 files skipped)
- One of the valid .txt files contains unique text: `project_alpha_unique_keyword`

## Test Data

- Toolkit: Artifact Toolkit, collection suffix: `skip-test`
- Search query: `project_alpha_unique_keyword`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Artifact Toolkit. Open the Test Settings panel on the right. Select `search_index` from the tool dropdown. | `search_index` tool is loaded with parameter fields. |
| 2 | Enter collection suffix `skip-test`. Set query to `project_alpha_unique_keyword`. Click Run Tool. | Tool executes. Result panel appears. |
| 3 | Examine results for content from the valid .txt file. | At least one result references the .txt file containing the unique keyword. |
| 4 | Scan results for any "Error during content parsing for file" messages. | No parsing error messages appear. |
| 5 | Verify no content citations reference the corrupted, unsupported, or password-protected files. | Search results contain no content from problematic files. |

## Expected Final State

Search results contain no content from problematic files.

## Pass/Fail Criteria

**Pass:**
- Relevant content from valid files returned
- No parsing error entries in results
- No content from problematic files in results

**Fail:**
- Zero results returned despite indexed valid content
- Parsing error entries from skipped files appear in results
- Content from corrupted or unsupported files is visible
