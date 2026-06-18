---
id: ELITEA-1221
title: "SharePoint Toolkit — Indexing /teams/ Space with Parametrized File Types and Path Scoping"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1221: SharePoint Toolkit — Indexing /teams/ Space with Parametrized File Types and Path Scoping

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that Index data on a /teams/ Site Path correctly applies Include Extensions and Skip Extensions filters across multiple file types, and that sub-folder path scoping produces isolated, correct results. Covers 4 sub-scenarios: (1) Include Extensions allowlist, (2) Skip Extensions denylist, (3) Path-scoped to sub-folder, (4) Combined Path + Include Extensions filter.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, PgVector and Embedding Model configured, Index data and Search index tools enabled
- Document library contains files of all listed types in both Shared Documents/Reports and Shared Documents/Archive

## Test Data

Site Path: teams/TestTeam
File types in Reports: .docx, .pdf, .xlsx, .xml, .md, .png (exclusion check)
File types in Archive: .docx, .pdf, .xlsx, .json, .md, .txt
Sub-scenarios: (1) Include allowlist, (2) Skip denylist for .xlsx/.pptx, (3) Path=Shared Documents/Reports, (4) Path=Shared Documents/Reports + Include=[.docx,.md]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open toolkit Indexes tab → + Create New Index. Set Include Extensions to [".docx",".pdf",".xlsx",".pptx",".json",".xml",".md",".txt"]. Leave Path and Skip Extensions empty. Start indexing. | Indexing completes without errors. Progress reaches 100%. |
| 2 | In Search Index, query for content unique to each of the 8 included file types. | Results are returned for all 8 file types. |
| 3 | Query for content unique to a .png file in the library. | No results returned — .png was not in the Include list. |
| 4 | Create a new index. Leave Include Extensions empty. Set Skip Extensions to [".xlsx",".pptx"]. Start indexing. | Indexing completes without errors. |
| 5 | Query for content from .xlsx and .pptx files. | No results for either type. |
| 6 | Query for content from .docx, .pdf, .json, .xml, .md, .txt files. | Results returned for all 6 remaining types. |
| 7 | Create a new index. Set Path to Shared Documents/Reports. Leave all extension filters empty. Start indexing. | Indexing completes without errors. |
| 8 | Query for content known to exist only in Shared Documents/Archive (e.g., a unique .json file). | No results returned — path scoping excluded Archive. |
| 9 | Query for content from Shared Documents/Reports (e.g., a unique .xml file). | Results returned with correct source citation pointing to Shared Documents/Reports. |
| 10 | Repeat steps 7–9 with Path set to Shared Documents/Archive. | Only content from Archive is indexed; Reports-only content returns no results. |
| 11 | Create a new index. Set Path to Shared Documents/Reports and Include Extensions to [".docx",".md"]. Start indexing. | Indexing completes without errors. |
| 12 | Query for a .pdf known to exist in Shared Documents/Reports. | No results — .pdf excluded by Include Extensions filter. |
| 13 | Query for .docx and .md content from Shared Documents/Reports. | Results returned for both types. |
| 14 | Query for .docx content known to exist only in Shared Documents/Archive. | No results — excluded by path scope. |

## Expected Final State

No results — excluded by path scope.

## Pass/Fail Criteria

Pass:
- All 8 included types are indexed and searchable in sub-scenario 1
- Excluded types (.png, .xlsx, .pptx) produce no search results when filtered out
- Path scoping isolates content to the specified folder only
- Combined filter produces correctly bounded results

Fail:
- A filtered-out file type appears in search results
- Content from outside the specified path scope appears in results
- Indexing fails or returns an error for the /teams/ site
- Any sub-scenario produces HTTP 500 or unhandled exception
