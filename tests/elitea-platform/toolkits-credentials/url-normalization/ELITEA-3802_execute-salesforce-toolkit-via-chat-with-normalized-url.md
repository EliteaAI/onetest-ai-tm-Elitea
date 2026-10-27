---
id: ELITEA-3802
title: "Execute Salesforce toolkit via Chat with normalized URL"
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
- Salesforce toolkit is configured with base_url containing trailing slash
- Check Connection for Salesforce toolkit passed successfully
- User has access to Chat interface

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Salesforce base_url | `https://company.my.salesforce.com/` (with trailing slash) |
| Salesforce object | Valid object name |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat interface | Chat page loads successfully |
| 2 | Start a new chat conversation | New chat session opened |
| 3 | Send message requiring Salesforce toolkit (e.g., "Query Account records with Status='Active'") | Message sent, AI processes |
| 4 | Observe Chat response and toolkit invocation | Chat shows toolkit invoked |
| 5 | Verify Salesforce toolkit executes without errors | Toolkit execution completes |
| 6 | Check Chat response for Salesforce data | Response contains valid data |
| 7 | Verify no URL-related error messages | No errors displayed |
| 8 | Send another message for different Salesforce operation | Message sent |
| 9 | Verify second Salesforce toolkit call succeeds | Tool executes, returns data |

## Expected Final State

- Salesforce toolkit tools execute successfully via Chat
- Chat displays valid Salesforce data
- No URL-related errors in Chat messages
- Multiple Salesforce tool invocations work in same session

## Pass/Fail Criteria

**Pass:**
- Salesforce toolkit invokes successfully from Chat
- Valid Salesforce data displayed in responses
- No URL-related error messages
- Multiple Salesforce tool calls succeed
- OAuth and REST API work correctly

**Fail:**
- Salesforce toolkit invocation fails from Chat
- URL-related error messages appear
- Malformed URLs cause failures
- Chat displays errors instead of data
