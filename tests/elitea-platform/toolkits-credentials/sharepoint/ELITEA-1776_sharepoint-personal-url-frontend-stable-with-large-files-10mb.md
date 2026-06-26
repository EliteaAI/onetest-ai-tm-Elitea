---
id: ELITEA-1776
title: "SharePoint Personal URL — Frontend Stable with Large Files (10MB+)"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, large-files, frontend-stability, bug-5212, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5212]
---
# ELITEA-1776: SharePoint Personal URL — Frontend Stable with Large Files (10MB+)

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that frontend remains responsive and does not crash or hang when reading large files (10-15MB) from personal SharePoint URLs via sharing links.

**Bug Coverage:** Regression test for bug #5212 — Frontend crash/hang with large files

## Preconditions

- Personal SharePoint credential configured and connected
- Large file (10-15MB PDF or DOCX) uploaded to personal SharePoint
- Sharing link generated for the large file
- Agent configured with SharePoint toolkit
- Browser developer console accessible for monitoring

## Test Data

- Test file: `large-report.pdf` (12-15MB, multi-page)
- Sharing link: Personal SharePoint sharing URL

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open browser developer console (F12) → Console tab | Console visible, monitoring for errors |
| 2 | Navigate to Chat with SharePoint-enabled agent | Chat interface opens |
| 3 | Send message: "Read this file: [personal-sharepoint-large-file-link]" | Agent processes request |
| 4 | Agent invokes "Read file from sharing link" tool | Tool execution starts, loading indicator appears |
| 5 | Monitor frontend behavior during processing (observe for 60 seconds) | Frontend remains responsive; Browser does not freeze; Loading indicator shows progress; Chat input remains accessible (may be disabled during tool execution) |
| 6 | Monitor browser console for errors | No crash errors in console; No "Out of memory" errors; No unhandled exceptions |
| 7 | Wait for tool completion or clear error response | Tool completes (or returns size limit error); Response appears in chat (content or error message) |
| 8 | Verify UI returns to normal interactive state | Chat input re-enabled; UI fully responsive; Can send additional messages |

## Expected Final State

Frontend remains stable; no crash or hang; UI returns to normal state

## Pass/Fail Criteria

**Pass:**
- Frontend remains responsive during large file processing
- No browser freeze or hang
- Loading indicator shows progress
- Tool completes with success or clear error (size limit exceeded)
- Browser console shows no crash-related errors
- UI returns to normal interactive state

**Fail:**
- Browser freezes or hangs indefinitely
- Tab becomes unresponsive (cannot interact with UI)
- Console shows crash errors or out-of-memory exceptions
- UI does not recover after tool execution
