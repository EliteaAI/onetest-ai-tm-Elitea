---
id: ELITEA-1781
title: "SharePoint Personal URL — Delegated Auth Read Document by Path (No 404)"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, delegated-auth, 404-error, bug-5323, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5323]
---
# ELITEA-1781: SharePoint Personal URL — Delegated Auth Read Document by Path (No 404)

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that "Read document" tool with document path does NOT return 404 error when using delegated authentication with personal SharePoint.

**Bug Coverage:** Regression test for bug #5323 — 404 error with delegated auth

## Preconditions

- Personal SharePoint credential configured with **delegated** authentication
- File uploaded to `/Shared Documents/` folder in personal SharePoint
- Agent configured with SharePoint toolkit

## Test Data

- File path: `/Shared Documents/test-file.pdf`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read the document at path: /Shared Documents/test-file.pdf" | Agent invokes "Read document" tool (by path, not sharing link) |
| 3 | Wait for tool execution | Tool processes request |
| 4 | Observe response | File content successfully retrieved; No error: "404 File not found"; No authentication error |
| 5 | Verify content displayed | Document content visible in response |

## Expected Final State

File content retrieved successfully using document path with delegated auth

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- File content retrieved
- No 404 error
- No "File not found" message

**Fail:**
- 404 error returned
- "File not found" despite file existing
- Authentication error
- Tool fails to locate file by path
