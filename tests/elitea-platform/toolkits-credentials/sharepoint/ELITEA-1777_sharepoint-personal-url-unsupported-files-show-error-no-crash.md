---
id: ELITEA-1777
title: "SharePoint Personal URL — Unsupported Files Show Error Without Crash"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, unsupported-files, error-handling, bug-5212, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5212]
---
# ELITEA-1777: SharePoint Personal URL — Unsupported Files Show Error Without Crash

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that attempting to read unsupported file types (MP4, ZIP) from personal SharePoint returns clear error message without causing frontend crash or hang.

**Bug Coverage:** Regression test for bug #5212 — Frontend crash with unsupported files

## Preconditions

- Personal SharePoint credential configured
- Unsupported files uploaded: MP4 video (5-10MB) and ZIP archive (3-5MB with images)
- Sharing links generated for both files
- Agent configured with SharePoint toolkit

## Test Data

- Test file 1: `video-sample.mp4` (video file)
- Test file 2: `archive-images.zip` (ZIP containing images)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with SharePoint-enabled agent | Chat opens |
| 2 | Send message: "Read this file: [mp4-sharing-link]" | Agent invokes tool |
| 3 | Observe error handling | Clear error message displayed: "Unsupported file type: .mp4" or similar; Frontend remains stable (no freeze) |
| 4 | Verify user can continue conversation | Chat input remains active; Can send new messages |
| 5 | Send message: "Read this file: [zip-sharing-link]" | Agent invokes tool |
| 6 | Observe error handling for ZIP file | Clear error displayed: "Unsupported file type: .zip"; Frontend stable |
| 7 | Check browser console for errors | No crash-related console errors |

## Expected Final State

Both unsupported files return clear errors; frontend remains stable

## Pass/Fail Criteria

**Pass:**
- Tool returns clear "Unsupported file type" error for both MP4 and ZIP
- Error messages displayed in agent response
- Frontend remains stable (no crash or hang)
- User can continue conversation after errors
- No console crash errors

**Fail:**
- Frontend crashes or hangs when processing unsupported files
- No error message or generic "Operation failed"
- UI becomes unresponsive
