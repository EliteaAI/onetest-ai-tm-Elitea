---
id: ELITEA-1784
title: "SharePoint Personal URL — Malformed URL Validation Error Propagated"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, url-validation, error-propagation, bug-5349, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5349]
---
# ELITEA-1784: SharePoint Personal URL — Malformed URL Validation Error Propagated

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that URL validation errors for malformed personal SharePoint URLs are clearly propagated to agent response and visible to user.

**Bug Coverage:** Regression test for bug #5349 — Validation errors not propagated

## Preconditions

- Personal SharePoint credential configured
- Agent configured with SharePoint toolkit

## Test Data

- Malformed URL 1: `my.sharepoint.com/:u:/r/personal/test.pdf` (missing `https://`)
- Malformed URL 2: `https://epam-my.sharepoint.com` (incomplete path)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read this file: my.sharepoint.com/:u:/r/personal/test.pdf" | Agent invokes tool |
| 3 | Observe error message in agent response | Clear validation error displayed in agent response; Error mentions: "Invalid URL format" or "URL must start with https://"; Error is propagated to user-visible response (not hidden) |
| 4 | Verify user can understand the issue | Error message explains what is wrong with the URL; User knows how to correct it |
| 5 | Test with second malformed URL | Send message with incomplete URL |
| 6 | Observe error for incomplete URL | Similar clear validation error displayed; Not generic "Operation failed" |

## Expected Final State

Clear validation errors displayed for malformed URLs

## Pass/Fail Criteria

**Pass:**
- Clear "Invalid URL format" error displayed in agent response
- Error mentions specific issue (missing https://, invalid format)
- Error is user-visible (propagated to response)
- User can understand what went wrong
- Not generic error message

**Fail:**
- Validation error hidden from user
- Generic "Operation failed" without details
- Error not propagated to agent response
- User cannot understand the issue
