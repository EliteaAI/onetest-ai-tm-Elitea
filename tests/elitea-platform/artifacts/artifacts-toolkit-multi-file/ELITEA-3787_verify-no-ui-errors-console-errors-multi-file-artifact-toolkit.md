---
id: ELITEA-3787
title: "Verify no UI error messages or console errors occur when agent saves multiple files via Artifact Toolkit"
priority: medium
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [r-2.0.4, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#5313]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with Artifact toolkit attached exists
- Browser DevTools console is open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Agent prompt | "Create and save 3 files: error-check-1.txt, error-check-2.txt, error-check-3.txt each with distinct content" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open browser DevTools → Console tab; clear existing logs | Console is clear |
| 2 | Navigate to the agent with Artifact toolkit and send the 3-file creation prompt | Agent processes the request |
| 3 | Monitor the browser console during and after the agent run | No red error entries appear in the console |
| 4 | Monitor the UI for any error toast notifications or inline error messages | No error toasts appear |
| 5 | Check the agent response for any "failed", "error", or "could not save" messages | Agent response confirms success without error language |
| 6 | Navigate to `{{base_url}}/app/artifacts` and verify all 3 files are present | All 3 files appear in the bucket |

## Expected Final State

The multi-file creation completes with no browser console errors, no UI error toasts, and no failure messages in the agent response. All 3 files are present in the artifact bucket.

## Pass/Fail Criteria

**Pass:**
- No JavaScript errors in browser console during agent run
- No error toast notifications in the UI
- Agent response contains no error or failure language
- All 3 files are present in the artifact bucket

**Fail:**
- One or more JavaScript errors appear in the browser console
- An error toast notification is displayed
- Agent response contains "failed", "error", or "could not save" language
