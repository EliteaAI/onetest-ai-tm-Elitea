---
id: ELITEA-1265
title: "Credential Form Validation — Required Fields Enforced Per Auth Mode"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1265: Credential Form Validation — Required Fields Enforced Per Auth Mode

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the credential form enforces required field validation appropriate to the selected auth mode and prevents saving incomplete credentials.

**Coverage:**
- App-only: Client Id, Client Secret, Site Url required; Oauth Discovery Endpoint NOT required
- Delegated: Client Id, Oauth Discovery Endpoint, Scopes, Site Url required
- Validation messages are displayed for each missing required field
- Save is blocked until all required fields for the active mode are filled

## Preconditions

- Logged in to `{{base_url}}
- SharePoint credential Create form open

## Test Data

- Empty form submission in each mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open SharePoint credential form. Select App-only mode. Leave ALL fields empty | Form in App-only mode with no data |
| 2 | Click Save | Validation errors appear for: Display Name (or ID), Client Id, Client Secret, Site Url. Oauth Discovery Endpoint does NOT show a validation error |
| 3 | Switch to Delegated mode. Leave ALL fields empty | Form in Delegated mode with no data |
| 4 | Click Save | Validation errors appear for: Display Name, Client Id, Oauth Discovery Endpoint, Scopes, Site Url |
| 5 | Fill in only Oauth Discovery Endpoint in Delegated mode. Leave Scopes empty | Partial form |
| 6 | Click Save | Validation error shown for Scopes (it is required in Delegated mode) |
| 7 | Fill in all required fields for App-only. Click Save | Credential saved successfully |
| 8 | Fill in all required fields for Delegated (but do NOT click Login). Click Save | Credential may save (token is separate from form fields). Behavior consistent with the design |

## Expected Final State

Credential may save (token is separate from form fields). Behavior consistent with the design

## Pass/Fail Criteria

**Pass:**
- App-only mode does not require Oauth Discovery Endpoint or Scopes
- Delegated mode requires Oauth Discovery Endpoint and Scopes
- Validation errors are shown per field
- Save is blocked for incomplete forms

**Fail:**
- App-only mode incorrectly requires Oauth Discovery Endpoint
- Delegated mode allows saving without Oauth Discovery Endpoint or Scopes
- No validation messages shown
- Form saves with missing required fields
