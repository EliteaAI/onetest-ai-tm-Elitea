---
id: ELITEA-1270
title: "Auth Subsection Labels Render as \"App-only\" and \"Delegated\""
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1270: Auth Subsection Labels Render as "App-only" and "Delegated"

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the credential form renders the correct renamed subsection labels "App-only" and "Delegated" (not the old labels "app_auth" and "delegated") across credential create and edit workflows.

**Coverage:**
- App-only label visible in the Auth radio group
- Delegated label visible in the Auth radio group
- No legacy labels (app_auth, App Auth, SECRET) shown to the user
- Labels correct in both Create and Edit credential views

## Preconditions

- Logged in to `{{base_url}}
- No existing SharePoint credentials required (test uses the Create form)

## Test Data

- Navigate to: `{{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to `{{base_url}}` → Click Add Credential → Select SharePoint | SharePoint credential form opens fresh |
| 2 | Scroll to the Auth section of the form | A radio button group is visible |
| 3 | Read the label of the first radio option | Label reads exactly App-only (not app_auth, App Auth, or SECRET) |
| 4 | Read the label of the second radio option | Label reads exactly Delegated (not delegated_auth or OAUTH) |
| 5 | Select App-only — inspect the form | Auth section remains at App-only, no extra OAuth fields shown |
| 6 | Select Delegated — inspect the form | Auth section switches to Delegated. OAuth fields (Oauth Discovery Endpoint, Scopes, Login button) appear |
| 7 | Open an existing SharePoint credential in Edit mode | Edit form loads |
| 8 | Verify the Auth radio group labels in Edit mode | Same App-only and Delegated labels as in Create mode |

## Expected Final State

Same App-only and Delegated labels as in Create mode

## Pass/Fail Criteria

**Pass:**
- Radio option 1 label: exactly App-only
- Radio option 2 label: exactly Delegated
- Labels are consistent across Create and Edit views
- No legacy/internal key names visible in the UI

**Fail:**
- Any label uses old naming (app_auth, delegated, App Auth, SECRET, OAUTH)
- Radio group missing entirely
- Labels differ between Create and Edit views
