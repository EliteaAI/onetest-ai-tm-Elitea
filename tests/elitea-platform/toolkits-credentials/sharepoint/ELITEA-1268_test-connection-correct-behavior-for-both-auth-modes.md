---
id: ELITEA-1268
title: "Test Connection — Correct Behavior for Both Auth Modes"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1268: Test Connection — Correct Behavior for Both Auth Modes

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Test Connection button correctly validates credentials for both App-only and Delegated auth modes, showing success or meaningful failure messages.

**Coverage:**
- App-only: Test connection succeeds with valid client_id + client_secret + site_url
- App-only: Test connection fails gracefully with invalid credentials
- Delegated: Test connection succeeds when a valid browser token is present
- Delegated: Test connection triggers re-auth prompt when no token is present

## Preconditions

- Valid Azure AD App Registration for both App-only and Delegated
- For Delegated: a valid token must be obtained via Login button first

## Test Data

- App-only valid credential: client_id=<valid>, client_secret=<valid>, site_url=<valid>
- App-only invalid credential: client_secret=INVALID_SECRET
- Delegated valid: token present after Login
- Delegated invalid: no token (cleared from session storage)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create/open a credential with App-only mode and valid client_id, client_secret, site_url | Form populated |
| 2 | Click Test connection | Success message: connection verified. No error |
| 3 | Change Client Secret to an invalid value INVALID_SECRET | Field updated |
| 4 | Click Test connection again | Failure message displayed (e.g., Authentication failed or Invalid client credentials). NOT a generic 500 error |
| 5 | Switch to Delegated mode. Clear token from session storage if present | No token in browser |
| 6 | Click Test connection without going through Login first | Message prompts user to authenticate first, or shows McpAuthorizationRequired-derived message |
| 7 | Click Login, complete OAuth consent | Token stored |
| 8 | Click Test connection | Success message for Delegated mode |

## Expected Final State

Success message for Delegated mode

## Pass/Fail Criteria

**Pass:**
- App-only connection test succeeds/fails appropriately based on credential validity
- Delegated connection test requires a valid browser token
- Error messages are specific (not generic 500s)
- Test connection uses the correct API path per mode

**Fail:**
- Test connection always shows success regardless of credential validity
- Delegated test connection ignores missing token
- Generic Internal Server Error shown instead of meaningful message
