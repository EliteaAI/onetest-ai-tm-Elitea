---
id: ELITEA-1787
title: "SharePoint Personal URL — Logout Functionality Disconnects Successfully"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, logout, session-management, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1787: SharePoint Personal URL — Logout Functionality Disconnects Successfully

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that "Logout" button successfully disconnects personal SharePoint credential and prevents further operations until re-authentication.

## Preconditions

- Personal SharePoint credential configured and connected
- User logged into {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials section | Credentials list displayed |
| 2 | Open personal SharePoint credential | Configuration page opens |
| 3 | Locate "Logout" button (usually near Test connection) | "Logout" button visible |
| 4 | Click "Logout" button | Disconnection process starts; Confirmation message may appear |
| 5 | Observe credential status change | Status changes to "Disconnected" or "Not authenticated"; OAuth token cleared/revoked |
| 6 | Attempt to use toolkit in chat after logout | Tool operation fails with authentication error: "Not authenticated" or "Please reconnect"; No file operation executes |
| 7 | Verify re-authentication option available | "Test connection" or OAuth flow can be initiated again |

## Expected Final State

Credential disconnected; operations blocked until re-authentication

## Pass/Fail Criteria

**Pass:**
- "Logout" button visible and functional
- Disconnection completes successfully
- Status changes to "Disconnected"
- Subsequent toolkit operations fail with auth error
- User can re-authenticate after logout

**Fail:**
- "Logout" button not visible
- Logout has no effect (still connected)
- Operations still work after logout
- Cannot re-authenticate
