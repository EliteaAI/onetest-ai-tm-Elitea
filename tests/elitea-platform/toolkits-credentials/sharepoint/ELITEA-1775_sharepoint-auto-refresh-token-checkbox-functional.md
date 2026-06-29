---
id: ELITEA-1775
title: "SharePoint Personal URL — Auto Refresh Token Checkbox Functional"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, oauth, token-refresh, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1775: SharePoint Personal URL — Auto Refresh Token Checkbox Functional

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Auto Refresh Token" checkbox is functional, persists after save, and enables automatic OAuth token renewal for personal SharePoint credentials.

## Preconditions

- Personal SharePoint credential being configured
- Delegated auth selected

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to SharePoint credential configuration page | Configuration form displayed |
| 2 | Locate "Auto Refresh Token" checkbox | Checkbox visible in OAuth configuration section |
| 3 | Check the "Auto Refresh Token" checkbox | Checkbox checked (checkmark visible) |
| 4 | Complete configuration and click "Save" | Configuration saved successfully |
| 5 | Close and re-open the credential configuration | Configuration page opens |
| 6 | Verify "Auto Refresh Token" checkbox state | Checkbox remains checked (state persisted) |
| 7 | Perform file operation immediately after save | Operation succeeds with valid token |
| 8 | Wait ~30-45 minutes (or until token near expiry if time allows) | N/A (time-based wait) |
| 9 | Perform another file operation without manual re-auth | Token auto-refreshes; Operation completes successfully; No "Token expired" error; No manual login prompt |

## Expected Final State

File operations continue without interruption; token refreshes automatically

## Pass/Fail Criteria

**Pass:**
- Checkbox visible and functional
- Checked state persists after save and reload
- Token auto-refreshes during operations (if testable within time constraints)
- No manual re-authentication required

**Fail:**
- Checkbox not visible or non-functional
- Checked state not persisted
- Token expires without auto-refresh (if testable)
- Manual re-auth required despite checkbox enabled

**Note:** Full token refresh behavior may require extended test time or simulated token expiry.
