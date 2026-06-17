---
id: ELITEA-1214
title: "SharePoint Index Data — Extension-Format skip_extensions Entries Still Exclude Files Correctly"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, eng:frontend, feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4897]
---
# ELITEA-1214: SharePoint Index Data — Extension-Format skip_extensions Entries Still Exclude Files Correctly

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that standard extension-format entries in `skip_extensions` (`.csv`, `csv`, `*.csv`) continue to exclude files correctly after the fix — no regression introduced.

**Coverage:**
- Three accepted input formats for `skip_extensions`: `.csv`, `csv`, `*.csv`
- All three formats produce identical exclusion behavior
- Non-skipped file types are unaffected

## Preconditions

- Logged in to {{base_url}} with Toolkit access
- SharePoint library contains: `ignored.csv`, `notes.docx`
- Index Data and Search Index tools enabled

## Test Data

- Skip Extensions (one per run): `[".csv"]`, `["csv"]`, `["*.csv"]`
- Include Extensions: empty (include all)
- Search filter 1: `{"Name": "ignored.csv"}`
- Search filter 2: `{"Name": "notes.docx"}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open + Create New Index; set Skip Extensions to [".csv"]; leave Include Extensions empty | Fields populated correctly |
| 2 | Run index and wait for completion | Indexing completes without errors |
| 3 | Search with filter {"Name": "ignored.csv"} | No results returned |
| 4 | Search with filter {"Name": "notes.docx"} | File found in results |
| 5 | Repeat Steps 1–4 with Skip Extensions = ["csv"] | Same exclusion result for .csv; notes.docx still indexed |
| 6 | Repeat Steps 1–4 with Skip Extensions = ["*.csv"] | Same exclusion result for .csv; notes.docx still indexed |

## Expected Final State

Same exclusion result for .csv; notes.docx still indexed

## Pass/Fail Criteria

**Pass:**
- `ignored.csv` returns no results in all three format runs
- `notes.docx` is found in all three runs
- All three formats behave identically

**Fail:**
- Any format fails to exclude `ignored.csv`
- `notes.docx` is unexpectedly excluded
- Behavior differs between formats
