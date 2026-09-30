---
id: ELITEA-3514
title: "Credential Visibility Restricted by Project Permissions"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3514: Credential Visibility Restricted by Project Permissions

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Outlook credentials (Client ID/Secret/tokens) are only visible/manageable to users with appropriate permissions on the project.

## Preconditions

- Two ELITEA user accounts on the same project: User A with credential-configuration permission, User B without it

## Test Data

- User A: has credential-configuration permission
- User B: no credential-configuration permission

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User A, create and authorize an Outlook credential in the shared project | Credential is created and authorized |
| 2 | Switch to User B on the same project | User B is logged in |
| 3 | As User B, attempt to view, edit, or reveal the stored Client Secret or token details for the credential | Access is denied / details are hidden |

## Expected Final State

The credential remains fully visible/manageable to User A and inaccessible (or read-restricted) to User B.

## Pass/Fail Criteria

**Pass:**
- User B cannot view, edit, or reveal Client Secret/token details

**Fail:**
- User B can view or edit the credential's sensitive fields despite lacking permission
