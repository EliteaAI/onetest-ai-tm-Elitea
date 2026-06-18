---
id: ELITEA-1263
title: "Existing App-only Credentials Pre-Selection Preserved on Edit"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1263: Existing App-only Credentials Pre-Selection Preserved on Edit

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when editing an existing App-only SharePoint credential, the App-only radio button is pre-selected and all App-only field values are retained.

**Coverage:**
- Edit view of an App-only credential shows App-only as selected auth mode
- Previously saved Client Id, Site Url are pre-filled
- Client Secret field is shown (though value may be masked)
- No OAuth fields shown for App-only credentials in Edit mode

## Preconditions

- An existing App-only SharePoint credential (e.g., sp-regression-apponly from TC-01)
- Logged in as Owner

## Test Data

- Credential name: `sp-regression-apponly`
- Edit URL: `/credentials/all/{id}?viewMode=owner`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to credentials list. Locate sp-regression-apponly | Credential listed |
| 2 | Click Edit on the credential | Edit form opens |
| 3 | Verify the Auth radio group | App-only radio is selected. Delegated is not selected |
| 4 | Verify the Client Id field has the previously saved value pre-filled | Client Id is shown |
| 5 | Verify Site Url pre-filled | Site Url is shown |
| 6 | Confirm Oauth Discovery Endpoint and Scopes fields are NOT visible | No OAuth fields for App-only mode |
| 7 | Make no changes. Click Save | Credential saved without errors. No data loss |

## Expected Final State

Credential saved without errors. No data loss

## Pass/Fail Criteria

**Pass:**
- App-only pre-selected on edit of App-only credential
- All App-only fields retain their saved values
- No OAuth fields shown in edit view for App-only mode
- Save without changes does not corrupt the credential

**Fail:**
- Auth mode defaults to Delegated on edit of App-only credential
- Previously saved fields are cleared or missing
- OAuth fields shown for App-only credentials in Edit mode
