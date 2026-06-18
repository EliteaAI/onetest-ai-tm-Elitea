---
id: ELITEA-0578
title: "Support Assistant — Unsupported File Types Are Rejected With a Clear Error Message"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0578: Support Assistant — Unsupported File Types Are Rejected With a Clear Error Message

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching unsupported file types (e.g., .exe, .bat) via drag-and-drop produces a clear, user-readable error listing allowed extensions, the file is not attached, and valid files added prior to the rejection are unaffected.

**Coverage:**
- .exe rejected via drag-and-drop with clear error
- .bat rejected via drag-and-drop with clear error
- Error message is user-readable (lists allowed types or names unsupported type)
- Unsupported file is NOT stored in the Artifacts attachments bucket
- Valid files attached before rejection remain unaffected

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- Test files: test.exe (< 1 KB), test.bat (< 1 KB), valid.png (< 1 MB)

## Test Data

- test.exe (< 1 KB, unsupported)
- test.bat (< 1 KB, unsupported)
- valid.png (< 1 MB, supported)
- Artifacts bucket: attachments

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Composer visible |
| 2 | Drag test.exe from OS file explorer and drop it onto the compose area | File rejected. Clear error banner: "Invalid file type: .exe is not supported" or listing allowed extensions. No thumbnail appears for test.exe. |
| 3 | Drag test.bat from OS file explorer and drop onto compose area | File rejected. Same clear error displayed. No thumbnail. |
| 4 | Attach valid.png first via click-to-browse (thumbnail appears), then attempt to drag test.exe onto compose area | valid.png thumbnail remains (unaffected). test.exe is rejected with the same error. |
| 5 | Type "Please review this image." and send with only valid.png attached | Message sent successfully. Bot responds. |
| 6 | Navigate to Artifacts → attachments bucket and verify test.exe is absent | test.exe is not present in the attachments bucket. |

## Expected Final State

test.exe is not present in the attachments bucket.

## Pass/Fail Criteria

**Pass:**
- .exe and .bat files are rejected with a clear, user-readable error
- No thumbnail appears for unsupported files
- Previously attached valid files are unaffected by the rejection
- Unsupported files are not stored in Artifacts

**Fail:**
- .exe or .bat is silently accepted
- Error message is absent or cryptic
- Rejection removes or corrupts previously attached valid files
- Unsupported file appears in Artifacts despite UI rejection
