---
id: ELITEA-1222
title: "SharePoint Toolkit — File Upload, List, and Read via /teams/ Site Path"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1222: SharePoint Toolkit — File Upload, List, and Read via /teams/ Site Path

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that Upload file, Get files list, and Read document tools work end-to-end against a /teams/ site for .txt, .docx, and .pdf file types. Covers: file upload to /teams/ document library folder; uploaded file appears in Get files list; Read document returns correct content for each file type.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, Upload file, Get files list, Read document tools enabled
- Target folder Shared Documents/QA exists in the /teams/ site
- Test files available in ELITEA Artifacts: test.txt, test.docx, test.pdf

## Test Data

Site Path: teams/TestTeam
Files: test.txt, test.docx, test.pdf (from ELITEA Artifacts)
Target folder: Shared Documents/QA

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Test Settings, select Upload file. Set folder path: Shared Documents/QA, file source: test.txt from Artifacts. Click Run Tool. | Success response. No HTTP 4xx/5xx error. |
| 2 | Select Get files list, scope to Shared Documents/QA. Click Run Tool. | test.txt appears in the returned file list. |
| 3 | Select Read document, provide the server-relative path of test.txt. Click Run Tool. | File content is returned and matches the uploaded test.txt. |
| 4 | Repeat steps 1–3 for test.docx. | Upload succeeds; file appears in list; Read document returns the .docx content. |
| 5 | Repeat steps 1–3 for test.pdf. | Upload succeeds; file appears in list; Read document returns the .pdf content. |
| 6 | Verify none of the three operations returned errors referencing an incorrect site URL. | No 'site not found', no /sites/ path in error messages for any file type. |

## Expected Final State

No 'site not found', no /sites/ path in error messages for any file type.

## Pass/Fail Criteria

Pass:
- All three file types upload, list, and read without errors
- Get files list shows each uploaded file in the /teams/ target folder
- Read document returns correct content for each file type

Fail:
- Any file type fails to upload or produces an HTTP error
- Uploaded file does not appear in Get files list
- Read document returns empty content or wrong content
- Any tool error references a /sites/ URL when Site Path points to /teams/
