---
id: ELITEA-0350
title: "read_multiple_files via Agent on multiple files each ≤200k chars — all files returned fully"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0350: read_multiple_files via Agent on multiple files each ≤200k chars — all files returned fully

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that read_multiple_files on multiple files each individually within the 200k limit returns all files fully — per-file check applies, no combined-total limit exists.

**Coverage:**
- Each file within 200k limit individually
- All files in the batch returned successfully
- No combined-total size check — batch of 3 × 80k = 240k total still succeeds
- Per-file enforcement correctly scoped

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Agent configured with Artifact Toolkit
- Three test files pre-uploaded to the bucket: `file_a.txt` (~80k), `file_b.txt` (~80k), `file_c.txt` (~80k)
- Combined total ~240k — above the per-file 200k limit if it were applied to the sum

## Test Data

- Files: `file_a.txt`, `file_b.txt`, `file_c.txt` (~80k chars each, ~240k total)
- Agent prompt: `"Read file_a.txt, file_b.txt, and file_c.txt and return all their contents"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent configured with the Artifact Toolkit. | Agent chat panel opens. |
| 2 | Send prompt: "Read file_a.txt, file_b.txt, and file_c.txt and return all their contents" | Agent invokes read_multiple_files with all three file paths. |
| 3 | Inspect the Agent response. | Content of all three files is returned fully. No size-limit error for any of them. Combined total (~240k) does not trigger any error. |

## Expected Final State

Content of all three files is returned fully. No size-limit error for any of them. Combined total (~240k) does not trigger any error.

## Pass/Fail Criteria

**Pass:**
- All 3 files returned fully with no size-limit error
- Response contains content from all three files

**Fail:**
- Any file returns a size-limit error string
- Combined-total check incorrectly blocks the batch
