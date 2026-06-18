---
id: ELITEA-1266
title: "Upload File Via Graph API — Small and Large Files"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1266: Upload File Via Graph API — Small and Large Files

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Upload file tool works correctly in Delegated auth mode for both small files (<4 MB, simple PUT) and large files (>5 MB, chunked resumable upload session).

**Coverage:**
- Small file upload (<4 MB) uses simple HTTP PUT to Graph API
- Large file upload (>5 MB) uses Graph API resumable upload session (createUploadSession)
- Files appear in SharePoint document library after upload
- Both upload paths work for Delegated (Graph API) mode

## Preconditions

- sp-delegated-oauth credential with valid token
- Toolkit with Upload file tool enabled
- Test files: `small-test.txt` (~10 KB), `large-test.bin` (>5 MB)
- SharePoint document library accessible

## Test Data

- Small file: `small-test.txt` (10 KB)
- Large file: `large-test.bin` (6 MB binary)
- Target folder: `Elitea-Test-Uploads`
- Agent prompt small: `Upload the file small-test.txt to SharePoint folder Elitea-Test-Uploads`
- Agent prompt large: `Upload the file large-test.bin to SharePoint folder Elitea-Test-Uploads`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent using the delegated SharePoint toolkit. | Ready |
| 2 | Trigger upload of small-test.txt with prompt: Upload small-test.txt to Elitea-Test-Uploads | Tool is invoked |
| 3 | Navigate to SharePoint document library and verify small-test.txt is present and verify the folder file path | File is visible in SharePoint & folder path is correct as specified in the tool |
| 4 | Trigger upload of large-test.bin (>5 MB) via agent | Tool is invoked for large file |
| 5 | Navigate to SharePoint and verify large-test.bin is present | File appears in SharePoint document library |
| 6 | Verify file sizes match (not truncated) | Uploaded file size matches source file size |

## Expected Final State

Uploaded file size matches source file size

## Pass/Fail Criteria

**Pass:**
- Small file: single PUT to Graph API, file appears in SharePoint
- Large file: createUploadSession + chunked upload, file appears in SharePoint with correct size
- No errors in agent response

**Fail:**
- Upload fails with auth error
- Large file upload falls back to simple PUT (wrong path)
- Files do not appear in SharePoint after upload
- File size mismatch (truncated upload)
