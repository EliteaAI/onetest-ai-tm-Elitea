---
id: ELITEA-3798
title: "SharePoint Personal URL — Delegated Auth Flow Completes Successfully"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, delegated-auth, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-3798: SharePoint Personal URL — Delegated Auth Flow Completes Successfully

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that delegated authentication flow completes successfully for personal SharePoint URLs (e.g., `https://epam-my.sharepoint.com/personal/username/`) and establishes a valid connection.

**Coverage:**
- Personal SharePoint URL format accepted in Site URL field
- OAuth delegated auth flow completes without errors
- Test connection validates successfully
- Credential saved and persists

## Preconditions

- User has access to {{base_url}} (e.g., dev.elitea.ai)
- User has valid personal SharePoint account credentials
- Azure App Registration configured with delegated auth permissions
- Client ID and Client Secret available

## Test Data

- Site URL: `https://epam-my.sharepoint.com/personal/your_username/`
- OAuth Discovery Endpoint: `https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration`
- Scopes: `Files.ReadWrite.All, Sites.ReadWrite.All, Sites.Selected, User.Read, Notes.ReadWrite.All`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials → Click "+ Credential" button | Credential creation form opens |
| 2 | Select "SharePoint" from credential type dropdown | SharePoint configuration form is displayed |
| 3 | Enter Display Name: "Personal SharePoint Test" | Field populated |
| 4 | Enter ID: "personal_sharepoint_test" | Field populated |
| 5 | Enter Client ID from Azure App Registration | Field populated (masked) |
| 6 | Enter Client Secret | Field populated (masked with dots) |
| 7 | Enter Site URL: `https://epam-my.sharepoint.com/personal/your_username/` | Personal URL format accepted without validation error |
| 8 | Select Auth Type: "Delegated" | Delegated selected from dropdown |
| 9 | Enter OAuth Discovery Endpoint | Field populated with Microsoft endpoint URL |
| 10 | Enter Scopes: `Files.ReadWrite.All, Sites.ReadWrite.All, Sites.Selected, User.Read, Notes.ReadWrite.All` | Scopes field populated |
| 11 | Check "Auto Refresh Token" checkbox | Checkbox checked |
| 12 | Click "Test connection" button | Loading spinner appears, OAuth popup window opens |
| 13 | Complete OAuth flow in popup (sign in, consent to permissions) | OAuth flow completes, popup closes automatically |
| 14 | Observe connection status on main page | Green checkmark or success message appears; "Connection successful" displayed |
| 15 | Click "Save" button and verify credential appears in credentials list | Credential saved; appears in list with "Connected" status |

## Expected Final State

Personal SharePoint credential is saved and shows "Connected" status in credentials list

## Pass/Fail Criteria

**Pass:**
- Personal SharePoint URL format accepted without validation errors
- OAuth flow completes successfully
- Test connection returns success status
- Credential persists after save
- No error messages displayed

**Fail:**
- Personal URL format rejected with validation error
- OAuth flow fails or hangs
- Test connection returns error
- Credential not saved or not visible in list
