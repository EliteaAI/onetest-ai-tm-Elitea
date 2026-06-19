---
id: ELITEA-1334
title: "Verify artifact file list updates without manual refresh after agent multi-file creation completes"
priority: high
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
- The Artifacts page for the configured bucket is open in the same browser session

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/artifacts` (bucket view open) |
| Agent prompt | "Create and save 3 files: refresh-test-1.txt, refresh-test-2.txt, refresh-test-3.txt each with distinct content" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Artifacts bucket page in one browser tab | Bucket file list is visible (may be empty or contain previous files) |
| 2 | In another tab or window, navigate to the agent and send the 3-file creation prompt | Agent confirms all 3 files were saved |
| 3 | Return to the Artifacts bucket tab and observe the file list without refreshing | All 3 new files appear in the list (auto-refresh) OR a "Refresh" indicator is shown |
| 4 | If files do not appear automatically, perform a manual page refresh | After refresh, all 3 files are visible |
| 5 | Confirm all 3 file names match the expected names | File names match exactly |

## Expected Final State

All 3 files created by the agent appear in the Artifacts bucket list, either immediately (auto-refresh) or after a single manual refresh.

## Pass/Fail Criteria

**Pass:**
- All 3 files appear in the bucket list after the agent completes (with or without manual refresh)
- File names match the expected values

**Fail:**
- Only 1 (or fewer than 3) files appear even after page refresh
- File list shows 0 files despite agent confirming successful creation
