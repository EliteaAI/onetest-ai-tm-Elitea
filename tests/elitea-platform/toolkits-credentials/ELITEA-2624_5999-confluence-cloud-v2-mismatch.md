---
id: ELITEA-2624
title: "[EliteaAI/elitea_issues#5999] Confluence Cloud + Forced v3 (Version Mismatch)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:confluence, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-2624: Confluence Cloud + Forced v3 (Mismatch Detection)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify behavior when Cloud instance is manually forced to unsupported API version.

## Preconditions

- Confluence Cloud instance (*.atlassian.net URL)
- Valid Cloud credentials
- Ability to force API version despite Cloud detection

## Test Data

| Config | Value |
|--------|-------|
| Hosting | Auto |
| Base URL | *.atlassian.net |
| API Version | 3 (forced/explicit, if unsupported) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Confluence toolkit with Cloud URL but force unsupported API Version. | Configuration saved (if allowed). |
| 2 | Click "Test Connection" button. | Connection test fails OR shows warning about mismatch. |
| 3 | If test succeeds despite mismatch: check error details. | Error message points to API/hosting mismatch (not generic auth error). |
| 4 | If config allowed to save: attempt a real content operation. | Operation fails OR returns incomplete data. |
| 5 | Verify error message clearly indicates the problem. | Message suggests checking API version or hosting selection. |
| 6 | Change API Version to Auto or correct version. | Re-test succeeds. |

## Expected Final State

- Mismatch detected in test or runtime
- Error message clear about incompatibility
- User guidance points to correct configuration
- Changing to compatible version resolves issue

## Pass/Fail Criteria

**Pass:** Mismatch detected, clear error, resolution succeeds.  
**Fail:** Silent failure, misleading error, no recovery path.

## Notes

- Tests error handling for incompatible configurations
- Validates user guidance is accurate
- Ensures mismatch caught early or clearly reported
