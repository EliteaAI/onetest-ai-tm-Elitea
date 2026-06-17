---
id: ELITEA-0291
title: "Reading or Previewing a Pre-Existing File with # in Its Filename Returns a Clear Error, Not a Generic 403"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3699]
---
# ELITEA-0291: Reading or Previewing a Pre-Existing File with # in Its Filename Returns a Clear Error, Not a Generic 403

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that previewing a legacy file with `#` in its filename (already present in the bucket before the fix) returns a descriptive, actionable error message — not a silent 403 or generic "Failed to fetch" — and the UI remains navigable afterward.

**Coverage:**
- Preview of pre-fix `test#.txt` triggers a meaningful error — not just "Failed to fetch file: 403"
- Error references `#` as the cause with actionable guidance
- Error is dismissible without a page reload
- UI remains fully navigable after the error

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome (latest)
- File `test#.txt` is already present in a bucket (uploaded before the fix — pre-fix legacy file)
- User has `configuration.artifacts.artifacts.view` permission

## Test Data

Bucket: tc-bucket
Pre-existing legacy file: test#.txt (contains #, uploaded pre-fix)
Error must NOT show only: "Failed to fetch file: 403"
Error must reference: # as the restricted/problematic character

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/ and open the Artifacts section. | Artifacts page is displayed. |
| 2 | Open the bucket containing `test#.txt`. | Bucket content list is displayed; `test#.txt` is visible in the file list. |
| 3 | Click the Preview (eye icon) next to `test#.txt`. | Preview action is triggered. |
| 4 | Observe the displayed error message. | An error message appears; it is NOT simply 'Failed to fetch file: 403' or a generic network error. |
| 5 | Read the error message text. | The message explicitly references `#` as the cause and includes actionable guidance related to the restriction (e.g., 'Filename contains restricted character #'). |
| 6 | Dismiss the error message. | Error message dismisses without requiring a full page reload. |
| 7 | Attempt to navigate to a different bucket or section within Artifacts. | Navigation succeeds; the page is fully responsive; no loading spinner persists. |

## Expected Final State

Navigation succeeds; the page is fully responsive; no loading spinner persists.

## Pass/Fail Criteria

**Pass:**
- An error message is displayed upon previewing `test#.txt`
- The error explicitly references `#` as the cause; it is NOT limited to "Failed to fetch file: 403"
- The error includes actionable language related to the restriction
- The error is dismissible without a page reload
- After dismissal, the UI is fully navigable and responsive

**Fail:**
- No error message is displayed; preview silently fails
- The error shows only "Failed to fetch file: 403" with no reference to `#`
- The UI becomes stuck requiring a page reload to proceed
- The preview panel opens but shows empty or broken content without any error message
