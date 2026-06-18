---
id: ELITEA-1269
title: "Auth Mode Switching — Conditional Field Visibility"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1269: Auth Mode Switching — Conditional Field Visibility

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching between App-only and Delegated auth modes shows/hides the correct set of fields in real time without page reload.

**Coverage:**
- App-only selected → Oauth Discovery Endpoint, Scopes, Login button are hidden
- Delegated selected → Oauth Discovery Endpoint (required), Scopes (required), Login button appear
- Client Secret field visibility per mode
- No stale/cached values from previous selection bleed into the active selection

## Preconditions

- Logged in to `{{base_url}}
- Navigate to SharePoint credential Create form

## Test Data

- Oauth Discovery Endpoint test value: `https://login.microsoftonline.com/test-tenant-id`
- Scopes test value: `sites.read.all user.read`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the SharePoint credential Create form | Form loads with default auth mode selected |
| 2 | Identify the initial (default) state of the Auth section | Note which option is default and which fields are visible |
| 3 | Select App-only radio button | Oauth Discovery Endpoint field is NOT visible. Scopes field is NOT visible. Login button is NOT visible. Client Secret field IS visible |
| 4 | Select Delegated radio button | Oauth Discovery Endpoint * field appears (marked required). Scopes * field appears (marked required). Login button appears. Fields animate in without page reload |
| 5 | Enter `https://login.microsoftonline.com/test-tenant-id` in Oauth Discovery Endpoint. Enter `sites.read.all user.read` in Scopes | Values accepted |
| 6 | Switch back to App-only | Oauth Discovery Endpoint and Scopes fields disappear. The entered values are no longer visible. Client Secret field is visible |
| 7 | Switch back to Delegated | Fields reappear. Verify whether previously entered values are restored or cleared (consistent UX expected) |

## Expected Final State

Fields reappear. Verify whether previously entered values are restored or cleared (consistent UX expected)

## Pass/Fail Criteria

**Pass:**
- Fields appear/disappear instantly on radio toggle without page reload
- App-only mode never shows OAuth-specific fields
- Delegated mode always shows Oauth Discovery Endpoint, Scopes, and Login
- Field visibility transitions are smooth (no layout shift errors)

**Fail:**
- Wrong fields shown for the selected mode
- Fields do not toggle on radio button change
- Values from one mode bleed into the other (stale data)
- Page reload required to see field changes
