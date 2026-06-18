---
id: ELITEA-1273
title: "Delegated OAuth — Complete In-Browser Login Flow"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1273: Delegated OAuth — Complete In-Browser Login Flow

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting Delegated auth mode, entering the OAuth discovery endpoint and scopes, and clicking Login produces a valid browser-stored access token.

**Coverage:**
- Delegated radio selection reveals OAuth fields
- Oauth Discovery Endpoint and Scopes fields are shown when Delegated is selected
- Login button initiates the Microsoft OAuth browser popup/redirect
- Successful OAuth consent results in a token stored in the browser session
- No error is shown after successful login

## Preconditions

- Logged in to `{{base_url}} as Owner
- Azure AD App Registration configured with delegated permissions: Sites.ReadWrite.All, Files.ReadWrite.All, User.Read
- OAuth Discovery Endpoint available: `https://login.microsoftonline.com/<tenant_id>`
- User account has access to the target SharePoint site

## Test Data

- Credential name: `sp-delegated-oauth`
- Client Id: `<delegated_app_client_id>`
- Oauth Discovery Endpoint: `https://login.microsoftonline.com/<tenant_id>`
- Scopes: `sites.read.all, user.read, files.read.all, sites.selected`
- Auth mode: `Delegated`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to `{{base_url}}` → Click Add Credential → Select SharePoint | Credential form opens |
| 2 | Fill in Display Name as `sp-delegated-oauth`, Client Id, and Site Url | Fields accept input |
| 3 | Locate the Auth radio group and select Delegated | Delegated is selected. Oauth Discovery Endpoint * and Scopes * input fields become visible. A Login button appears |
| 4 | Enter the Oauth Discovery Endpoint: `https://login.microsoftonline.com/<tenant_id>` | Field accepts the URL |
| 5 | Enter Scopes: `sites.read.all, user.read, files.read.all, sites.selected` | Scopes field accepts the comma-separated values |
| 6 | Click the Login button | A Microsoft authentication popup/redirect window opens. The URL contains the tenant login domain (login.microsoftonline.com) |
| 7 | Complete the Microsoft OAuth consent: enter credentials and approve permissions if prompted | Popup closes or redirects back. No error message is shown on the credential form |
| 8 | Verify the credential form shows a success indicator or the Login button state changes | UI indicates successful authentication (button may show different state or a success toast appears) |
| 9 | Click Test connection | Test connection succeeds (200 OK) confirming the stored token is valid |
| 10 | Click Save | Credential is saved. No error. Redirects to credential list with sp-delegated-oauth visible |

## Expected Final State

Credential is saved. No error. Redirects to credential list with sp-delegated-oauth visible

## Pass/Fail Criteria

**Pass:**
- Delegated selection shows Oauth Discovery Endpoint, Scopes, and Login fields
- Login button opens the Microsoft OAuth flow
- After consent, the token is stored in the browser session
- Test connection succeeds with the delegated token
- Credential saves without error

**Fail:**
- Login button does not open OAuth flow
- OAuth popup opens but results in an error (e.g., redirect URI mismatch, invalid client)
- No token is stored after OAuth consent
- Test connection fails after successful OAuth login
- Credential cannot be saved
