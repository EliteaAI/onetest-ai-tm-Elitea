---
id: ELITEA-3807
title: "Execute SonarQube toolkit via Chat with normalized URL"
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
- SonarQube toolkit is configured with url containing trailing slash
- Check Connection for SonarQube toolkit passed successfully
- User has access to Chat interface

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube url | `https://sonar.example.com/` (with trailing slash) |
| Project key | Valid SonarQube project key |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat interface | Chat page loads successfully |
| 2 | Start a new chat conversation | New chat session opened |
| 3 | Send message requiring SonarQube toolkit (e.g., "Get code quality metrics for project X") | Message sent, AI processes |
| 4 | Observe Chat response and toolkit invocation | Chat shows toolkit invoked |
| 5 | Verify SonarQube toolkit executes without errors | Toolkit execution completes |
| 6 | Check Chat response for SonarQube data | Response contains valid data |
| 7 | Verify no URL-related error messages | No errors displayed |
| 8 | Send another message for different SonarQube query | Message sent |
| 9 | Verify second SonarQube toolkit call succeeds | Tool executes, returns data |

## Expected Final State

- SonarQube toolkit tools execute successfully via Chat
- Chat displays valid SonarQube data
- No URL-related errors in Chat messages
- Multiple SonarQube tool invocations work in same session

## Pass/Fail Criteria

**Pass:**
- SonarQube toolkit invokes successfully from Chat
- Valid SonarQube data displayed in responses
- No URL-related error messages
- Multiple SonarQube tool calls succeed
- API path concatenation works correctly

**Fail:**
- SonarQube toolkit invocation fails from Chat
- URL-related error messages appear
- Malformed URLs cause failures
- Chat displays errors instead of data
