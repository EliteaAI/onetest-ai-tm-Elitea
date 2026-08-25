---
id: ELITEA-2623
title: "[EliteaAI/elitea_issues#5999] Confluence Server + Auto Mode (v2)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:confluence, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-2623: Confluence Server + Auto Mode (v2)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Confluence Server/Self-Hosted connection with Auto mode uses appropriate API version and content operations succeed.

## Preconditions

- Confluence Server/Self-Hosted instance available (non-.atlassian.net URL)
- Valid Server credentials (basic auth or personal access token)
- Confluence page available for testing
- Logging visible

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | on-premise.confluence.local (or similar) |
| API Version | Auto |
| Credentials | Valid Server credentials |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Confluence toolkit: Hosting=Auto, Base URL=on-premise URL, API Version=Auto. | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds. |
| 3 | Check logs: verify appropriate API version used for Server. | Logs show API v2 selection (Confluence Server standard). |
| 4 | Save configuration. | Configuration persisted. |
| 5 | In Chat/Agent, run a read operation (get page, search spaces). | Tool call succeeds; page/space data returned. |
| 6 | Run a write operation (create page or update content). | Page created/updated in Confluence Server. |
| 7 | Verify page appears in Confluence UI. | Page visible in Confluence. |

## Expected Final State

- Auto mode detects Server/Self-Hosted and uses appropriate API version
- Connection test and runtime both use same version
- Read and write operations work correctly
- No manual API version override needed

## Pass/Fail Criteria

**Pass:** Correct API version used automatically, no fallback needed, read/write both succeed.  
**Fail:** Wrong API version selected, runtime fails, manual override required.

## Notes

- Confluence Server typically uses REST API v2
- Tests Auto mode with Server deployment
- Validates both read and write operations
