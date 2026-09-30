---
id: ELITEA-3558
title: "Teams Credential Configuration UI Functions Correctly Despite Reusing Generic OAuth-Toolkit Components"
priority: high
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3558: Teams Credential Configuration UI Functions Correctly Despite Reusing Generic OAuth-Toolkit Components

**Module:** Teams Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify the Teams credential creation/edit form — which has no Teams-specific frontend component and relies on the shared delegated-OAuth toolkit UI used by SharePoint/Outlook — renders the correct label, fields, and icon, and functions end-to-end.

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit credentials
- At least one existing Teams credential available for the edit-flow check

## Test Data

- N/A (UI inspection and existing credential)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the credential creation form and select "Teams" | Toolkit label shown is "Teams" with the Teams icon; required fields (Azure AD Client ID, Client Secret, OAuth Discovery Endpoint, Scopes) are present and correctly grouped under the auth/Delegated section |
| 2 | Complete credential creation | No mislabeled fields or leftover text from another toolkit (e.g. SharePoint/Outlook wording) appear anywhere in the flow |
| 3 | Edit the existing Teams credential | Existing values load correctly into the form and can be updated and saved |

## Expected Final State

The Teams credential form behaves as a fully correct, Teams-branded instance of the shared OAuth component; edits persist correctly.

## Pass/Fail Criteria

**Pass:**
- Label, icon, and fields are all correctly Teams-specific with no cross-toolkit leakage
- Edit flow loads and saves existing values correctly

**Fail:**
- Any field, label, or icon is mislabeled, missing, or shows another toolkit's wording
- Edit flow fails to load or save existing values
