---
id: ELITEA-0358
title: "read_multiple_files with skip_size_check=False — 3 files each ≤200k but total >200k — all returned fully (no combined check)"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0358: read_multiple_files with skip_size_check=False — 3 files each ≤200k but total >200k — all returned fully (no combined check)

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when `skip_size_check=False` is passed to read_multiple_files and files individually are ≤200k chars but combined exceed 200k, all files are returned fully — confirming there is no combined-total size check, only per-file enforcement.

**Coverage:**
- `skip_size_check=False` passed explicitly
- Each individual file ≤200k → passes per-file check
- Combined total ~240k → no combined check exists, all files returned
- Per-file enforcement correctly scoped

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Artifact Toolkit accessible via Toolkit Test Settings
- Three test files pre-uploaded: `file_a.txt` (~80k), `file_b.txt` (~80k), `file_c.txt` (~80k)

## Test Data

- Files: `file_a.txt`, `file_b.txt`, `file_c.txt` (~80k each, ~240k total)
- Tool: `read_multiple_files`
- Parameters: `file_paths = ["file_a.txt", "file_b.txt", "file_c.txt"]`, `skip_size_check = false`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page. Open the Artifact Toolkit. Go to Test Settings panel. | Test Settings panel opens. |
| 2 | Select `read_multiple_files`. Enter the three file paths and set `skip_size_check = false`. Click Run. | Tool executes. |
| 3 | Inspect the response. | All three files returned fully. No size-limit error for any file. Combined total (~240k) does not trigger an error because each file individually is within the 200k per-file limit. |

## Expected Final State

All three files returned fully. No size-limit error for any file. Combined total (~240k) does not trigger an error because each file individually is within the 200k per-file limit.

## Pass/Fail Criteria

**Pass:**
- All 3 files returned fully
- No size-limit error for any individual file
- Combined total does not cause a batch-level error

**Fail:**
- Any file returns a size-limit error (each is ≤200k — should not be blocked)
- Batch incorrectly blocked due to a combined-total check
