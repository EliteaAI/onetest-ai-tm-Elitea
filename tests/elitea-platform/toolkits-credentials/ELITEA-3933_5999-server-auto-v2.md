---
id: ELITEA-3933
title: "[EliteaAI/elitea_issues#5999] Jira Server + Auto Mode (v2)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3933: Jira Server + Auto Mode (v2)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Jira Server/Self-Hosted connection with Auto mode uses API v2 and read/write operations succeed.

## Preconditions

- Jira Server/Self-Hosted instance available (non-.atlassian.net URL)
- Valid Server credentials (basic auth or personal access token)
- Jira issue available for testing
- Logging visible

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | on-premise.jira.local (or similar) |
| API Version | Auto |
| Credentials | Valid Server credentials |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Jira toolkit: Hosting=Auto, Base URL=on-premise URL, API Version=Auto. | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds. |
| 3 | Check logs: verify API v2 used (no v3 fallback). | Logs show "Using API v2" for Server/Self-Hosted. |
| 4 | Save configuration. | Configuration persisted. |
| 5 | In Chat/Agent, run a read operation (search or get issue). | Tool call succeeds; issue data returned. |
| 6 | Run a write operation (add comment). | Comment created in Jira Server. |
| 7 | Verify comment appears in Jira UI. | Comment visible in Jira. |
| 8 | Run an update operation (change field). | Field updated successfully. |

## Expected Final State

- Auto mode detects Server/Self-Hosted and uses API v2
- Connection test and runtime both use v2
- Read and write operations work correctly
- No manual API version override needed

## Pass/Fail Criteria

**Pass:** API v2 used automatically, no fallback, read/write both succeed.  
**Fail:** Wrong API version selected, runtime fails, manual override required.

## Notes

- Tests Auto mode with Server deployment
- Validates v2-specific behavior
- Ensures read and write both work (not just read)
