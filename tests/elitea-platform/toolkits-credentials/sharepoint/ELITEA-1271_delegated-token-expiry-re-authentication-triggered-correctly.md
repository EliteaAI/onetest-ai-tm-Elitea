---
id: ELITEA-1271
title: "Delegated Token Expiry — Re-Authentication Triggered Correctly"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1271: Delegated Token Expiry — Re-Authentication Triggered Correctly

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a delegated OAuth token is expired or absent, the platform raises McpAuthorizationRequired and prompts the user to re-authenticate via the browser Login flow.

**Coverage:**
- McpAuthorizationRequired exception raised by SharepointGraphWrapper on 401 responses
- User is redirected to or prompted to use the credential Login button
- After re-authentication, tool execution succeeds
- No silent failure or generic error message shown

## Preconditions

- A `sp-delegated-oauth` credential exists
- The token in the browser session has been cleared or has expired (use browser DevTools → Application → Session Storage to remove the token)
- A SharePoint toolkit using this credential is configured
- An agent using this toolkit is accessible

## Test Data

- Credential: `sp-delegated-oauth`
- Expired/removed token scenario: clear session storage entry keyed by `https://login.microsoftonline.com/<tenant_id>`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open DevTools → Application → Session Storage for dev.elitea.ai. Locate the token entry for the OAuth discovery endpoint and delete it | Token entry is removed from session storage |
| 2 | Navigate to the agent that uses the SharePoint delegated toolkit. Send prompt: List files in the document library | Agent attempts to invoke Get files list |
| 3 | Observe the response in the agent chat | Agent returns an authentication error or McpAuthorizationRequired message — NOT a generic crash. The error message should guide the user to re-authenticate |
| 4 | Navigate to `{{base_url}}` → Open sp-delegated-oauth | Credential form is displayed |
| 5 | Click the Login button | Microsoft OAuth popup opens |
| 6 | Complete authentication | Popup closes; token is stored in session storage again |
| 7 | Return to the agent and re-send the same prompt | Agent executes the tool successfully. File list is returned |

## Expected Final State

Agent executes the tool successfully. File list is returned

## Pass/Fail Criteria

**Pass:**
- Expired/missing token triggers McpAuthorizationRequired (not a 500 or unhandled error)
- Error message clearly indicates authentication is required
- After re-authenticating via Login button, tool executes successfully
- No data corruption or orphaned state after re-auth cycle

**Fail:**
- Tool crashes with unhandled exception instead of auth prompt
- No re-authentication mechanism is presented to user
- Tool silently returns empty results without indicating auth failure
- Credential form does not allow re-login after expiry
