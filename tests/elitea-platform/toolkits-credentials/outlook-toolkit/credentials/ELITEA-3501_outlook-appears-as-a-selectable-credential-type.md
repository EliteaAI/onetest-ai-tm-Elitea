---
id: ELITEA-3501
title: "Outlook Appears as a Selectable Credential Type"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3501: Outlook Appears as a Selectable Credential Type

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Outlook" appears in the Credential Type Selector on the Credentials page with its own icon and label, distinct from SharePoint/Teams/OpenAPI, and that selecting it renders the Outlook-specific form fields.

## Preconditions

- Logged in to `{{base_url}}` with permission to create credentials

## Test Data

- N/A (UI inspection only)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials → Create Credential | Credential Type Selector opens |
| 2 | Locate "Outlook" in the type selector | Outlook is listed with its own icon (`outlook.svg`) and label, visually distinct from SharePoint/Teams/OpenAPI |
| 3 | Select "Outlook" | Form renders Outlook-specific fields: Client ID, Client Secret, Mailbox, OAuth Discovery Endpoint, Scopes, Auto-refresh token, grouped under a "Delegated" section |

## Expected Final State

The Outlook credential creation form is open and displays all expected fields; no credential has been saved yet.

## Pass/Fail Criteria

**Pass:**
- Outlook is selectable with a distinct icon/label
- All documented fields render correctly under the "Delegated" grouping

**Fail:**
- Outlook is missing from the type selector, or reuses another toolkit's icon/label
- Any documented field is missing or mislabeled
