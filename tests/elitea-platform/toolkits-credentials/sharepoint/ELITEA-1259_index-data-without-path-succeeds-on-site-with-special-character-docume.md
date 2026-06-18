---
id: ELITEA-1259
title: "index_data Without Path Succeeds on Site With Special-Character Document Library Names"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1259: index_data Without Path Succeeds on Site With Special-Character Document Library Names

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that executing `index_data` from the SharePoint toolkit without specifying a `path` parameter completes successfully when the SharePoint site contains document libraries whose names include special characters.

**Coverage:**
- `index_data` invoked with `path` field left empty
- SharePoint site contains libraries: `doc-lib_for/sharepoint^retest()-/@!$-test~@#%^&*:;,.`, `sharepoint-index#1`, `hyphen-folder`
- Index status shows success (no "Index processing error" banner)
- Total indexed count is non-zero
- No `AttributeError: 'str' object has no attribute 'items'` is raised
- No "Tool execution failed" message is shown

## Preconditions

- Logged in to {{base_url}} as a user with Owner or Editor role in a Private project
- SharePoint toolkit configured with valid Azure AD Client ID and Client Secret pointing to the test SharePoint site
- SharePoint site contains document libraries: `doc-lib_for/sharepoint^retest()-/@!$-test~@#%^&*:;,.`, `sharepoint-index#1`, `hyphen-folder` — each with at least data.txt and file.xlsx
- PgVector and Embedding Model configured in Settings → AI Configuration
- Index Data tool is enabled in the toolkit configuration

## Test Data

- Index Name: `nopath`
- Path field: (empty — leave blank)
- Clean Index: unchecked
- Progress Step: 10
- Limit Files: 1000

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select the SharePoint toolkit | SharePoint toolkit detail page opens |
| 2 | Click the Indexes tab | Indexes tab opens, showing existing indexes (if any) |
| 3 | Click the + button (New Index) | New Index form appears on the right panel with empty fields |
| 4 | Enter `nopath` in the Index Name field | Name field shows `nopath` |
| 5 | Leave the Path field completely empty | Path field is blank |
| 6 | Click the Index button | Indexing job starts; index entry appears in the left list with a progress indicator |
| 7 | Wait for the indexing job to complete | Index status transitions from in-progress to completed |
| 8 | Check the status indicator on the index entry | No "Index processing error" banner is shown; success state is displayed |
| 9 | Check the total indexed counter next to the index entry | Counter shows a non-zero number reflecting the files in the SharePoint site |

## Expected Final State

Counter shows a non-zero number reflecting the files in the SharePoint site

## Pass/Fail Criteria

**Pass:**
- Indexing completes without error
- Total indexed count is ≥ 1
- No `AttributeError` or "Tool execution failed" message appears

**Fail:**
- "Index processing error" banner is shown
- Total indexed count is 0 or displays an error
- `AttributeError: 'str' object has no attribute 'items'` appears in output
- "Tool execution failed" message is returned
