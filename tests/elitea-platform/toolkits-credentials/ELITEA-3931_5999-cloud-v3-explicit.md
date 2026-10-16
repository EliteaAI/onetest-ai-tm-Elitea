---
id: ELITEA-3931
title: "[EliteaAI/elitea_issues#5999] Jira Cloud + Explicit API v3"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3931: Jira Cloud + Explicit API v3

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify explicit API v3 selection works for Cloud and ADF-based operations (comments, creation) function correctly.

## Preconditions

- Same Jira Cloud instance as ELITEA-2616
- Valid Cloud credentials
- Jira issue available for testing (to add comment, update)

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | *.atlassian.net |
| API Version | 3 (explicit) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Jira toolkit: API Version=3 (explicit, not Auto). | Configuration saved. |
| 2 | Click "Test Connection" button. | Connection test succeeds. |
| 3 | Check logs: verify API v3 used directly (no v2 attempt). | Logs show "Using API v3 (explicit)" or similar. |
| 4 | Save configuration. | Configuration persisted. |
| 5 | In Chat/Agent, run a read operation (search or get issue). | Tool call succeeds; issue data returned. |
| 6 | Run a write operation (add comment with ADF formatting). | Comment created successfully in Jira. |
| 7 | Verify comment appears in Jira UI and preserves ADF formatting (bold, lists, etc.). | ADF formatting intact in Jira. |
| 8 | If available, run an update operation (change field value). | Field updated successfully in Jira. |

## Expected Final State

- Explicit v3 selection enforced (no fallback to v2)
- Connection test and runtime both use API v3
- Read and write operations work with ADF payloads
- No mismatch between test connection and runtime behavior

## Pass/Fail Criteria

**Pass:** Explicit v3 used, no v2 attempt, ADF operations work, read/write both succeed.  
**Fail:** Fallback attempted despite explicit v3, ADF formatting lost, write operation fails.

## Notes

- Tests that explicit version override works
- Validates ADF-based operations (v3 feature)
- Ensures consistency: explicit = no fallback
