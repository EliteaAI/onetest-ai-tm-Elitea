---
id: ELITEA-0351
title: "read_file with start_line and end_line on large file returns correct slice — no regression"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0351: read_file with start_line and end_line on large file returns correct slice — no regression

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that partial reads using start_line and end_line still work correctly on large files after the skip_size_check change — no regression in line-range slicing behavior.

**Coverage:**
- start_line / end_line parameters correctly slice a large file
- Only the requested range is returned, not the full file
- Slice result matches expected lines from the known file content

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Artifact Toolkit accessible via Toolkit Test Settings
- Test file `xlarge_file.txt` (~300k chars) with known content at specific line numbers pre-uploaded

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Tool: `read_file`
- Parameters: `filename = xlarge_file.txt`, `start_line = 100`, `end_line = 110`
- Expected: exactly lines 100–110 of the file returned

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkit Test Settings. Select `read_file`. Enter `filename = xlarge_file.txt`, `start_line = 100`, `end_line = 110`. Click Run. | Tool executes with line range parameters. |
| 2 | Inspect the response. | Response contains exactly 11 lines (lines 100–110 of the file). Content matches the known lines at that position. Full file is not returned. |

## Expected Final State

Response contains exactly 11 lines (lines 100–110 of the file). Content matches the known lines at that position. Full file is not returned.

## Pass/Fail Criteria

**Pass:**
- Correct line range returned (lines 100–110)
- Content matches known file content at those lines
- Full file not returned

**Fail:**
- Wrong lines returned
- Full file returned instead of slice
- Error or empty response
