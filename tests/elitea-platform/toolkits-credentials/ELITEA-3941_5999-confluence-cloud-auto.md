---
id: ELITEA-3941
title: "[EliteaAI/elitea_issues#5999] Confluence Cloud + Auto Mode Happy Path"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:confluence, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3941: Confluence Cloud + Auto Mode Happy Path

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Confluence Cloud connection works with Auto API version selection and runtime content operations match connection test result.

## Preconditions

- Confluence Cloud instance available (*.atlassian.net domain)
- Valid Confluence Cloud credentials (username/API token)
- Toolkit configuration interface accessible
- Agent/Chat interface available for content operations
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
| 1 | Configure Confluence toolkit: Hosting=Auto, Base URL=cloud.atlassian.net, API Version=Auto. | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds (green checkmark). |
| 3 | Check logs: verify API version attempted (Confluence REST API v2 or v3). | Logs show API version selection. |
| 4 | Save toolkit configuration. | Configuration persisted. |
| 5 | In Chat/Agent, call a read Confluence tool (e.g., get page, search pages). | Tool call succeeds with content returned. |
| 6 | Verify runtime used same API version as test. | Tool execution logs match connection test logs. |
| 7 | Verify page/content data returned is accurate. | Returned data (page content, metadata) match Confluence Cloud. |

## Expected Final State

- Connection test passes
- Auto mode selects appropriate API version for Cloud
- Toolkit configuration saved without manual version override
- Runtime content operations succeed using discovered API version
- No manual configuration edits needed after connection test

## Pass/Fail Criteria

**Pass:** Test connection succeeds, correct API version selected, runtime tools work without config changes.  
**Fail:** Connection fails, wrong API version, runtime differs from test, manual config needed.

## Notes

- Confluence Cloud typically uses v2 REST API with expansion capability
- Tests the happy path for Auto mode with Cloud
- Runtime consistency is critical
