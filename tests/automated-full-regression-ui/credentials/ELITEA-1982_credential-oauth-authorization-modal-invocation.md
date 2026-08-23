---
id: ELITEA-1982
title: "Credential — OAuth Authorization Modal Invocation"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_oauth_authorization_modal.TestCredentialOAuthAuthorizationModal.test_oauth_authorization_modal_invocation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1714
---

# ELITEA-1982: Credential — OAuth Authorization Modal Invocation

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the Login button on a SharePoint Delegated credential opens the "Configuration OAuth" dialog with the correct pre-populated fields, and that cancelling the dialog closes it without taking action.

---

## Preconditions

- User is logged in to the Elitea platform.
- A SharePoint credential with Delegated auth type exists and has Oauth Discovery Endpoint and Scopes configured.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | SharePoint |
| Auth method | Delegated |
| Expected dialog title | Configuration OAuth |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing SharePoint credential with Delegated auth type | Credential detail page loads |
| 2 | Verify the "Login" button is present next to "Test connection" | Login button is visible |
| 3 | Click the "Login" button | "Configuration OAuth" dialog appears |
| 4 | Verify the dialog shows the message: "This MCP server requires OAuth authorization to access its tools." | Message is displayed in the dialog |
| 5 | Verify the "Server:" field shows the Oauth Discovery Endpoint URL as a clickable link | Server field is populated with the endpoint URL as a link |
| 6 | Verify the "Scope (optional)" field is pre-populated with credential scopes prefixed by "offline_access" | Scope field contains "offline_access" followed by the credential scopes |
| 7 | Verify the scope placeholder text: "Enter OAuth scopes (space-separated)" | Placeholder text is correct when field is empty |
| 8 | Verify "Cancel" and "Authorize" buttons are present in the dialog | Both buttons are visible |
| 9 | Click "Cancel" | Dialog closes without taking any action |

---

## Expected Final State

The OAuth dialog opens correctly with pre-populated server and scope fields; cancelling dismisses the dialog without initiating authorization.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Dialog displays the correct message, server URL, and pre-populated scopes; Cancel closes the dialog without action.

**Fail:**
- Any step produces an error or unexpected result.
- Dialog does not open, fields are not pre-populated, or Cancel triggers an authorization attempt.
