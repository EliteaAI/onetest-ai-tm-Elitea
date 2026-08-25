---
id: ELITEA-2627
title: "[EliteaAI/elitea_issues#5999] Confluence Explicit v2 (Server/Cloud Compatibility)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:confluence, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-2627: Confluence Explicit v2 (Server/Cloud Compatibility)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify explicit v2 selection works for both Confluence Server and Cloud instances that support v2 API.

## Preconditions

- Confluence instance available (Server or Cloud with v2 support)
- Valid credentials
- Confluence page/space available for testing

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | Any Confluence instance |
| API Version | 2 (explicit) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Confluence toolkit: API Version=2 (explicit, not Auto). | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds. |
| 3 | Check logs: verify API v2 used (no version fallback). | Logs show "Using API v2 (explicit)". |
| 4 | Save configuration. | Configuration persisted. |
| 5 | In Chat/Agent, run a read operation (get page, search). | Tool call succeeds; page data returned. |
| 6 | Run a write operation (create page or update content). | Page created/updated successfully. |
| 7 | Verify content appears/updates in Confluence UI. | Changes visible in Confluence. |

## Expected Final State

- Explicit v2 enforced (no fallback or version negotiation)
- Connection test and runtime both use API v2
- Read and write operations work with v2 API
- Works consistently for both Server and Cloud v2-compatible instances

## Pass/Fail Criteria

**Pass:** Explicit v2 used consistently, no fallback, read/write both succeed.  
**Fail:** Wrong API version used, fallback attempted, read/write fails.

## Notes

- Tests explicit version override
- Validates v2 API operations work
- Ensures consistency: explicit = no negotiation
