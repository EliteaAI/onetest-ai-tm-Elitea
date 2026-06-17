---
id: ELITEA-1274
title: "App-only Authentication Regression After OAuth Deployment"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1274: App-only Authentication Regression After OAuth Deployment

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that existing SharePoint App-only (client credentials) authentication continues to work without breaking after the OAuth/Delegated flow changes are deployed.

**Coverage:**
- App-only credential with `client_id` + `client_secret` still authenticates correctly
- `Get files list` tool returns results using App-only credentials
- No regression in legacy REST-based SharePoint operations
- Subsection label "App-only" renders correctly in credential form

## Preconditions

- Logged in to `{{base_url}} as Owner
- A pre-existing SharePoint credential configured with App-only (`client_id`, `client_secret`, `site_url`) exists or can be created
- An Azure AD App Registration with `Sites.Read.All` application permission is available

## Test Data

- Credential name: `sp-regression-apponly`
- Client Id: `<app_only_client_id>`
- Client Secret: `<app_only_client_secret>`
- Site Url: `https://<tenant>.sharepoint.com/sites/<site>`
- Auth mode: `App-only`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to `https://dev.elitea.ai/app/credentials` | Credentials list is displayed |
| 2 | Click Add Credential → Select credential type SharePoint | SharePoint credential form opens |
| 3 | Fill in Display Name as `sp-regression-apponly`, Client Id, Client Secret, and Site Url | Fields accept input without errors |
| 4 | Locate the Auth radio group. Verify two options are visible: App-only and Delegated | Radio group with both options is present; App-only is selectable |
| 5 | Select App-only radio button | App-only is selected. The Oauth Discovery Endpoint and Scopes fields are NOT visible. The Login button is NOT visible |
| 6 | Click Test connection | Success message is displayed (connection to SharePoint site verified) |
| 7 | Click Save | Credential is saved. Redirects back to credential list. sp-regression-apponly entry is visible |
| 8 | Navigate to `https://dev.elitea.ai/app/toolkits/create/sharepoint?viewMode=owner` | SharePoint toolkit creation page loads |
| 9 | Enter toolkit name sp-apponly-toolkit, select credential sp-regression-apponly in the SharePoint Configuration dropdown | Credential is selected. Toolkit form is valid |
| 10 | Enable the Get files list tool in the TOOLS section | Tool toggle is ON |
| 11 | Click Save | Toolkit is saved without errors |
| 12 | Navigate to an agent that uses this toolkit. Invoke the tool with prompt: List all files in the SharePoint document library | Agent executes the tool. A list of files from the SharePoint site is returned |

## Expected Final State

Agent executes the tool. A list of files from the SharePoint site is returned

## Pass/Fail Criteria

**Pass:**
- App-only radio option is visible and selectable
- No Oauth Discovery Endpoint, Scopes, or Login elements appear when App-only is selected
- Test connection succeeds for App-only credentials
- Get files list tool returns actual file data from SharePoint via REST client
- No JavaScript errors or 500 responses in browser console

**Fail:**
- App-only credential cannot connect (401, 403, or SDK error)
- App-only credential form is missing or broken after OAuth changes
- Get files list returns an empty list or error when files exist
- Any regression in existing App-only flow
