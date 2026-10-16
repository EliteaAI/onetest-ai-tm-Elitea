---
id: ELITEA-3935
title: "[EliteaAI/elitea_issues#5999] Cloud URL + Forced API v2 (Mismatch)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3935: Cloud URL + Forced API v2 (Mismatch Detection)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify behavior when Cloud URL is manually forced to API v2 (incompatible configuration).

## Preconditions

- Jira Cloud instance (*.atlassian.net URL)
- Valid Cloud credentials
- Ability to force API version v2 despite Cloud detection

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | *.atlassian.net |
| API Version | 2 (forced/explicit) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Jira toolkit with Cloud URL but force API Version=2. | Configuration saved (if allowed). |
| 2 | Click "Test Connection" button. | Connection test fails OR shows warning about mismatch. |
| 3 | If test succeeds despite mismatch: check error details. | Error message points to API/hosting mismatch (not generic auth error). |
| 4 | If config allowed to save: attempt a real tool call in Chat/Agent. | Tool call fails OR returns incomplete data. |
| 5 | Verify error message clearly indicates the problem. | Message suggests checking API version or hosting selection. |
| 6 | Change API Version to Auto or 3. | Re-test succeeds. |

## Expected Final State

- Mismatch between Cloud URL and v2 is detected
- Error message is clear about the incompatibility (not just "auth failed")
- User guidance points to correct configuration
- Changing to compatible version resolves the issue

## Pass/Fail Criteria

**Pass:** Mismatch detected in test or runtime, clear error, resolution succeeds.  
**Fail:** Silent failure, misleading error message, no recovery path.

## Notes

- Tests error handling for incompatible configurations
- Validates user guidance is accurate
- Ensures mismatch is caught early (test connection) or clearly reported in runtime
