---
id: ELITEA-1227
title: "SharePoint Credential with Full /teams/ URL — Test Connection Success"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1227: SharePoint Credential with Full /teams/ URL — Test Connection Success

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that a SharePoint credential whose Site URL contains a full /teams/ path reports a successful Test Connection and allows toolkit tools to retrieve data. Covers: /teams/ URL accepted without validation error; Test Connection returns success; toolkit using this credential (empty Site Path) retrieves files from the /teams/ site.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- App registration with Client ID and Client Secret having permissions on https://your-tenant.sharepoint.com/teams/test-team
- /teams/test-team has at least one document

## Test Data

- Credential Display Name: SharePoint Teams Creds
- Site URL: https://your-tenant.sharepoint.com/teams/test-team
- Client ID: (valid app registration value)
- Client Secret: (valid secret)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials → + Create → SharePoint. Fill in: Display Name 'SharePoint Teams Creds', Site URL 'https://your-tenant.sharepoint.com/teams/test-team', Client ID and Client Secret. | Form accepts all values. No validation error on the Site URL field for the /teams/ format. |
| 2 | Click Test Connection. | Result shows Success. No authentication error, no 'site not found', no timeout. |
| 3 | Click Save. | Credential is saved. No error toast. |
| 4 | Navigate to Toolkits → + Create → SharePoint. Select credential 'SharePoint Teams Creds'. Leave Site Path empty. Enable Get files list. Click Save. | Toolkit is saved successfully. |
| 5 | Open the toolkit, go to Test Settings, select Get files list, click Run Tool. | Files from .../teams/test-team are returned. No HTTP errors. |

## Expected Final State

Files from .../teams/test-team are returned. No HTTP errors.

## Pass/Fail Criteria

Pass:
- /teams/ URL accepted in the Site URL field without validation error
- Test Connection returns success
- Toolkit tools retrieve data from the /teams/ site with no errors

Fail:
- Credential form rejects the /teams/ URL format
- Test Connection returns an error for a valid /teams/ credential
- Toolkit tools fail or return data from a wrong site
