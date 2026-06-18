---
id: ELITEA-0357
title: "skip_size_check=False explicitly passed — single file >200k returns size-limit error"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0357: skip_size_check=False explicitly passed — single file >200k returns size-limit error

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that passing `skip_size_check=False` explicitly to read_file enforces the 200k limit — a file exceeding 200k chars returns the size-limit error string even on paths that would otherwise be uncapped.

**Coverage:**
- Explicit `skip_size_check=False` overrides the default True behavior
- File >200k returns `[Content has N lines and exceeds size limit...]`
- Per-file enforcement — only the file exceeding 200k is affected

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Artifact Toolkit accessible via Toolkit Test Settings
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the bucket

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Tool: `read_file`
- Parameters: `filename = xlarge_file.txt`, `skip_size_check = false`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page. Open the Artifact Toolkit. Go to Test Settings panel. | Test Settings panel opens. |
| 2 | Select `read_file`. Enter `filename = xlarge_file.txt` and set `skip_size_check = false`. Click Run. | Tool executes with the explicit parameter. |
| 3 | Inspect the response. | Response contains the size-limit error string: `[Content has N lines and exceeds size limit. Use partial read options.]` — not the full file content. |

## Expected Final State

Response contains the size-limit error string: `[Content has N lines and exceeds size limit. Use partial read options.]` — not the full file content.

## Pass/Fail Criteria

**Pass:**
- Size-limit error string returned when `skip_size_check=False` and file >200k
- Opt-in enforcement works correctly

**Fail:**
- Full content returned despite `skip_size_check=False` (enforcement broken)
- Different error unrelated to content size
