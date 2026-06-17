---
id: ELITEA-1234
title: "[#4660] SharePoint — Reactive 401 Auto-Refresh and Retry for READ and WRITE Operations"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, feat:toolkits, issue:4660, int:oauth, 401-retry, r-2.0.3]
requirements: [4660]
---
# ELITEA-1234: [#4660] SharePoint — Reactive 401 Auto-Refresh and Retry for READ and WRITE Operations

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a SharePoint API call returns 401 Unauthorized (expired access token but valid refresh token), the backend automatically calls `_try_refresh_token()`, obtains a new access token, and retries the original operation — for both read (GET) and write (POST/DELETE/PUT/PATCH) operations. Previously only GET had this retry; POST, DELETE, file upload, and OneNote operations now also retry.

## Preconditions

SharePoint toolkit authenticated with a valid refresh token stored in sessionStorage
Access token has been manually expired (set `access_token` to null or expired value in sessionStorage, or wait for natural expiry)
Refresh token is still valid

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With an expired access token (but valid refresh token in sessionStorage), trigger a READ SharePoint tool call via Agent Chat — e.g., 'list files in my Documents folder' using an agent with SharePoint toolkit. | The tool call executes successfully. File list is returned in chat. No 'Logon' button appears. Backend received 401 → refreshed token → retried GET → success. |
| 2 | Again with an expired access token, trigger a WRITE operation — e.g., 'upload this file to SharePoint' or 'create a folder named TestFolder' via Agent Chat. | Write operation (POST/PUT) executes successfully. No 'Logon' prompt shown. Backend received 401 → refreshed → retried POST/PUT → success. |
| 3 | With an expired access token, trigger a DELETE operation — e.g., 'delete the file TestFile.txt from SharePoint'. | Delete operation executes successfully. No login interruption. |
| 4 | With an expired access token, trigger a file upload operation on a large file (>4 MB to exercise chunked upload path). | File upload completes successfully. Each chunk that hits 401 is retried with the refreshed token. Upload result is confirmed. |

## Expected Final State

File upload completes successfully. Each chunk that hits 401 is retried with the refreshed token. Upload result is confirmed.

## Pass/Fail Criteria

READ operation (GET) auto-refreshes and retries on 401 → success
WRITE operation (POST/PUT) auto-refreshes and retries on 401 → success
DELETE operation auto-refreshes and retries on 401 → success
Large file chunked upload auto-refreshes and retries on 401 per chunk → upload completes
No 'Logon' prompt shown to user for any of the above when refresh token is valid
