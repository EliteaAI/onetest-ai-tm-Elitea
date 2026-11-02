---
id: ELITEA-3794
title: "Execute Jira toolkit via Chat with normalized URL"
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
- Jira toolkit is configured with base_url containing trailing slash (e.g., `https://jira.example.com/`)
- Check Connection for Jira toolkit passed successfully
- User has access to Chat interface with toolkit invocation capability

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url | `https://jira.example.com/` (with trailing slash) |
| Jira project key | Valid project key |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat interface | Chat page loads successfully |
| 2 | Start a new chat conversation | New chat session opened |
| 3 | Send a message that requires Jira toolkit invocation (e.g., "Search for open issues in project TEST") | Message sent, AI processes request |
| 4 | Observe Chat response and toolkit invocation | Chat shows toolkit is being invoked |
| 5 | Verify Jira toolkit executes without errors | Toolkit execution completes successfully |
| 6 | Check Chat response for Jira data | Response contains valid Jira issue data |
| 7 | Verify no error messages related to URL format | No URL-related errors displayed in Chat |
| 8 | Send another message requiring different Jira tool (e.g., "Get details of issue TEST-123") | Message sent |
| 9 | Verify second Jira toolkit call also succeeds | Tool executes and returns valid data |

## Expected Final State

- Jira toolkit tools execute successfully via Chat interface
- Chat displays valid Jira data in responses
- No URL-related errors appear in Chat messages
- Multiple Jira tool invocations work correctly in the same chat session

## Pass/Fail Criteria

**Pass:**
- Jira toolkit invokes successfully from Chat interface
- Valid Jira data is displayed in Chat responses
- No URL-related error messages appear
- Multiple Jira tool calls succeed in same session
- Jira client initializes correctly with normalized URL

**Fail:**
- Jira toolkit invocation fails from Chat
- Error messages related to URL format appear in Chat
- Malformed URLs cause toolkit failures
- Chat displays errors instead of Jira data
