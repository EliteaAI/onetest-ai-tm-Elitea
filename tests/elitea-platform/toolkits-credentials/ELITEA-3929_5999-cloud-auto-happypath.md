---
id: ELITEA-3929
title: "[EliteaAI/elitea_issues#5999] Jira Cloud + Auto Mode Happy Path"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3929: Jira Cloud + Auto Mode Happy Path

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Jira Cloud connection works with Auto API version selection and runtime tool execution matches connection test result.

## Preconditions

- Jira Cloud instance available (atlassian.net domain)
- Valid Jira Cloud credentials (username/API token)
- Toolkit configuration interface accessible
- Agent/Chat interface available for tool execution
- Logging visible to verify API version used

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | *.atlassian.net |
| API Version | Auto |
| Credentials | Valid Cloud API token |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Jira toolkit: Hosting=Auto, Base URL=cloud.atlassian.net, API Version=Auto. | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds (green checkmark). |
| 3 | Check logs: verify API v2 attempted first. | Logs show "Attempting API v2" for Jira Cloud. |
| 4 | Check logs: verify fallback to API v3 occurred. | Logs show "Fallback to API v3" with success. |
| 5 | Save toolkit configuration. | Configuration persisted. |
| 6 | In Chat/Agent, call a read Jira tool (e.g., search issues, get issue). | Tool call succeeds with results returned. |
| 7 | Verify runtime used same API version as test. | Tool execution logs match connection test logs (API v3 used). |
| 8 | Verify issue data returned is accurate. | Returned data (fields, values) match Jira Cloud. |

## Expected Final State

- Connection test passes
- Auto mode falls back from v2 to v3 for Cloud
- Toolkit configuration saved without manual version override
- Runtime tool execution succeeds using discovered API version
- No manual configuration edits needed after connection test

## Pass/Fail Criteria

**Pass:** Test connection succeeds, API v3 used (after v2 attempt), runtime tools work without config changes.  
**Fail:** Connection fails, no fallback, runtime differs from test, manual config needed.

## Notes

- This validates the happy path for Auto mode with Cloud
- Fallback behavior is critical: must attempt v2 then v3
- Runtime consistency is key: tool execution should match connection test
