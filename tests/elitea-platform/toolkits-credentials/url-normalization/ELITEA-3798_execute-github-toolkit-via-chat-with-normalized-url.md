---
id: ELITEA-3798
title: "Execute GitHub toolkit via Chat with normalized URL"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- GitHub toolkit is configured with base_url containing trailing slash
- Check Connection for GitHub toolkit passed successfully
- User has access to Chat interface

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| GitHub base_url | `https://github.example.com/api/v3/` (with trailing slash) |
| Repository | Valid repository name |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat interface | Chat page loads successfully |
| 2 | Start a new chat conversation | New chat session opened |
| 3 | Send message requiring GitHub toolkit (e.g., "List files in repository owner/repo") | Message sent, AI processes |
| 4 | Observe Chat response and toolkit invocation | Chat shows toolkit invoked |
| 5 | Verify GitHub toolkit executes without errors | Toolkit execution completes |
| 6 | Check Chat response for GitHub data | Response contains valid data |
| 7 | Verify no URL-related error messages | No errors displayed |
| 8 | Send another message for different GitHub tool | Message sent |
| 9 | Verify second GitHub toolkit call succeeds | Tool executes, returns data |

## Expected Final State

- GitHub toolkit tools execute successfully via Chat
- Chat displays valid GitHub data
- No URL-related errors in Chat messages
- Multiple GitHub tool invocations work in same session

## Pass/Fail Criteria

**Pass:**
- GitHub toolkit invokes successfully from Chat
- Valid GitHub data displayed in responses
- No URL-related error messages
- Multiple GitHub tool calls succeed
- GitHub client initializes correctly

**Fail:**
- GitHub toolkit invocation fails from Chat
- URL-related error messages appear
- Malformed URLs cause failures
- Chat displays errors instead of data
