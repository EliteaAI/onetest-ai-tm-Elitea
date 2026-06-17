---
id: ELITEA-0722
title: "All-Unsupported-Files Bucket: Indexing Reaches a Clean Terminal State Without Crashing"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0722: All-Unsupported-Files Bucket: Indexing Reaches a Clean Terminal State Without Crashing

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that indexing a bucket where every file is unparseable terminates on its own  — no infinite spinner, no application crash, no unhandled exception.

**Coverage:**
- Indexing does not get stuck in 🔄 In Progress indefinitely
- No application crash banner or unhandled exception dialog shown
- An informative message indicates that files could not be processed

## Preconditions

- Logged in to {{base_url}}
- Artifact Toolkit with `all-invalid-test` bucket: 3 files — all unsupported or corrupted, no valid files

## Test Data

- Bucket: `all-invalid-test`
- Files: `bad1.exe` (renamed as .pdf), `bad2.docx` (corrupted header), `bad3.pdf` (password-protected)
- Expected document count: `0`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact Toolkit → Indexes Tab. Create a new index for `all-invalid-test` (suffix: `inval`). Click Index. | Status changes to 🔄 In Progress. |
| 2 | Wait for the job to reach a terminal state without manually stopping it (allow up to standard indexing timeout). | Job terminates on its own. Does NOT remain in 🔄 In Progress indefinitely. |
| 3 | Check that the page is stable — no crash banner or unhandled exception dialog visible. | Page is stable. No fatal error shown. |
| 4 | Check the progress log or run messages for a summary of the all-skipped outcome. | A message is present indicating no files could be processed (e.g., "3 files skipped"). |

## Expected Final State

A message is present indicating no files could be processed (e.g., "3 files skipped").

## Pass/Fail Criteria

**Pass:**
- Job reaches a terminal state without manual intervention
- No application crash or unhandled exception
- Document count = 0
- User-visible message about zero processed files present

**Fail:**
- Job remains in 🔄 In Progress indefinitely
- Application crashes or shows unhandled exception
- Document count incorrectly shows a non-zero value
