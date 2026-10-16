---
id: ELITEA-3786
title: "Verify file timestamps are populated and valid for all files created in a multi-file agent run"
priority: medium
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [r-2.0.4, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#5313]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with Artifact toolkit attached exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/artifacts` |
| Agent prompt | "Create and save 3 files: ts-test-1.txt, ts-test-2.txt, ts-test-3.txt each with distinct content" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the agent and send the 3-file creation prompt | Agent confirms all 3 files saved |
| 2 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list is displayed |
| 3 | Locate ts-test-1.txt, ts-test-2.txt, and ts-test-3.txt in the file list | All 3 files are present |
| 4 | For each file, inspect the timestamp/date column | Timestamp is populated (not blank, not epoch 1970-01-01, not a future date) |
| 5 | Verify all 3 timestamps fall within the current date/time window (within the last 10 minutes) | Timestamps are recent and accurate |

## Expected Final State

All 3 files have valid, non-zero, recent timestamps displayed in the Artifacts UI.

## Pass/Fail Criteria

**Pass:**
- All 3 files show a populated timestamp
- Timestamps are recent (within 10 minutes of the test execution time)

**Fail:**
- Any file shows a blank, zero, or epoch timestamp
- Any timestamp is in the distant past or future
