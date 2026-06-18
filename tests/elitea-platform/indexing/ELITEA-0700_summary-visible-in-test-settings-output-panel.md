---
id: ELITEA-0700
title: "Summary Visible in Test Settings Output Panel"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0700: Summary Visible in Test Settings Output Panel

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that indexing triggered via the Test Settings panel produces the structured summary in the output panel, not just a generic completion message.

**Coverage:**
- Output panel shows ✅ Successfully indexed N documents (M chunks). line
- Output panel shows ⚠️ and/or ❌ sections with file names for any non-success files
- Summary is produced via Test Settings the same way as via Indexes tab

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- Bucket contains a mix of valid and skipped/failed files

## Test Data

- Bucket: summary-mix-test; collection suffix: ts01
- Files: 3 valid .txt, 1 empty-content PDF (empty.pdf), 1 corrupted .docx

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → open the Artifacts toolkit → locate the TEST SETTINGS panel on the right side of the page. | Test Settings panel is visible. |
| 2 | From the tool dropdown, select Index Data. | Index Data parameter form appears. |
| 3 | Enter collection suffix ts01; leave all other fields at defaults. | Parameters filled. |
| 4 | Click Run Tool. | Execution starts; output panel shows progress. |
| 5 | Wait for execution to complete. | Output panel shows the final result. |
| 6 | Verify the output includes ✅ Successfully indexed 3 documents (M chunks). | Line present; count = 3. |
| 7 | Verify the output includes a ⚠️ section listing empty.pdf and a ❌ section listing the corrupted file. | Both sections present with correct file names. |

## Expected Final State

Both sections present with correct file names.

## Pass/Fail Criteria

**Pass:**
- Output panel shows the full structured summary with ✅/⚠️/❌ sections
- File names in non-success sections match known skipped/failed files

**Fail:**
- Output panel shows only a generic success/error string without a per-section breakdown
- ⚠️/❌ sections absent for known non-success files
