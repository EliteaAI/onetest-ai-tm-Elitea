---
id: ELITEA-1981
title: "Credential — OAuth-Required Credential Flow (SharePoint Delegated)"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1981: Credential — OAuth-Required Credential Flow (SharePoint Delegated)

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting the Delegated auth type for a SharePoint credential reveals the correct OAuth-specific fields, that the credential saves successfully, and that the Login button remains available on the saved credential page.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | SharePoint |
| Auth method | Delegated |
| Client Id | (any placeholder value) |
| Client Secret | (any placeholder value) |
| Site Url | (any valid or placeholder URL) |
| Oauth Discovery Endpoint | (any valid or placeholder URL) |
| Scopes | (any valid or placeholder scopes) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Credentials section | Credentials list page loads |
| 2 | Create a new credential of type "SharePoint" | SharePoint-specific form fields are displayed |
| 3 | Select the "Delegated" radio button for Auth | Delegated-specific fields appear |
| 4 | Verify additional fields appear: Auto Refresh Token checkbox, Oauth Discovery Endpoint, Scopes | All Delegated auth fields are visible |
| 5 | Verify a "Login" button appears next to the "Test connection" button | Login button is visible in the form |
| 6 | Fill in all required fields: Client Id, Client Secret, Site Url, Oauth Discovery Endpoint, Scopes | All fields accept the input |
| 7 | Save the credential | Credential is saved successfully with Delegated auth type |
| 8 | Verify the "Login" button remains available on the saved credential detail page | Login button is present on the detail page |

---

## Expected Final State

The SharePoint Delegated credential is saved with all OAuth fields populated, and the Login button is available on the credential detail page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Delegated auth fields are shown when selected; credential saves successfully; Login button is present on the detail page.

**Fail:**
- Any step produces an error or unexpected result.
- Delegated auth fields do not appear, credential fails to save, or Login button is missing.
