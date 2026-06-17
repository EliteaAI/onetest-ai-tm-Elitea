---
id: ELITEA-1256
title: "index_data With Explicit Path on Special-Character Library Names Still Works (Regression)"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1256: index_data With Explicit Path on Special-Character Library Names Still Works (Regression)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that providing an explicit path to a library with special characters does not break indexing after the fix — ensuring the path-specified flow is not regressed.

**Coverage:**
- `index_data` invoked with an explicit server-relative path pointing to a special-character library
- Path-specified indexing completes successfully after the fix
- Total indexed count is non-zero and matches files in the specified library
- No `AttributeError` or unhandled exception is thrown

## Preconditions

- Logged in to {{base_url}} as a user with Owner or Editor role in a Private project
- SharePoint toolkit configured with valid Azure AD Client ID and Client Secret
- Library `doc-lib_for/sharepoint^retest()-/@!$-test~@#%^&*:;,.` contains uploaded files
- Server-relative path to this library is known (e.g., from the SharePoint admin URL)
- PgVector and Embedding Model configured in Settings → AI Configuration
- Index Data tool is enabled

## Test Data

- Index Name: `regpath`
- Path field: server-relative path to the special-character library (exact path from the SharePoint admin URL)
- Expected file count: number of files previously uploaded to that library

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select the SharePoint toolkit → open the Indexes tab | Indexes tab is displayed |
| 2 | Click + (New Index) | New Index form appears |
| 3 | Enter `regpath` in Index Name | Name field shows `regpath` |
| 4 | In the Path field, enter the full server-relative path to the special-character library | Path field shows the entered value |
| 5 | Click Index | Indexing job starts |
| 6 | Wait for the job to complete | Job completes without error |
| 7 | Check the index status and total indexed counter | No error banner; counter matches the number of files in the specified library |
| 8 | Confirm no AttributeError in the output | No error traceback is visible |

## Expected Final State

No error traceback is visible

## Pass/Fail Criteria

**Pass:**
- Indexing with explicit path completes successfully
- Total indexed count matches files in the specified library
- No `AttributeError` or crash occurs

**Fail:**
- "Index processing error" appears
- `AttributeError` is raised
- Total indexed count is 0 or incorrect
