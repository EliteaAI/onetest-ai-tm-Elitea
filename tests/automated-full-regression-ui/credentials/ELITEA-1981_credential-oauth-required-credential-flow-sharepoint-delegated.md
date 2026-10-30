---
id: ELITEA-1981
title: "OAuth E2E Journey — SharePoint Delegated"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1981: OAuth E2E Journey — SharePoint Delegated

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify the complete OAuth credential lifecycle: creation with Delegated auth fields, OAuth authorization modal invocation, successful authorization with redirect and token storage, Login→Logout button change, Test connection success, credential token persistence across navigation and toolkit integration, and graceful error handling for failed OAuth flows.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.
- Valid OAuth provider credentials are available for completing the login flow (Microsoft account for SharePoint).
- A SharePoint toolkit is available or can be created.

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
| Valid scopes | (any valid or placeholder scopes, e.g., "Sites.Read.All") |
| Invalid scope | Invalid.Scope.xyz |
| OAuth provider credentials | (valid Microsoft account credentials) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **SETUP Phase: Create SharePoint Delegated Credential** | | |
| 1 | Navigate to the Credentials section | Credentials list page loads |
| 2 | Create a new credential of type "SharePoint" | SharePoint-specific form fields are displayed |
| 3 | Select the "Delegated" radio button for Auth | Delegated-specific fields appear |
| 4 | Verify additional fields appear: Auto Refresh Token checkbox, Oauth Discovery Endpoint, Scopes | All Delegated auth fields are visible |
| 5 | Verify a "Login" button appears next to the "Test connection" button | Login button is visible in the form |
| 6 | Fill in all required fields: Client Id, Client Secret, Site Url, Oauth Discovery Endpoint, Scopes | All fields accept the input |
| 7 | Save the credential | Credential is saved successfully with Delegated auth type |
| 8 | Verify the "Login" button remains available on the saved credential detail page | Login button is present on the detail page |
| **OAUTH MODAL Phase** | | |
| 9 | Click the "Login" button | "Configuration OAuth" dialog appears |
| 10 | Verify the dialog shows the message: "This MCP server requires OAuth authorization to access its tools." | Message is displayed in the dialog |
| 11 | Verify the "Server:" field shows the Oauth Discovery Endpoint URL as a clickable link | Server field is populated with the endpoint URL as a link |
| 12 | Verify the "Scope (optional)" field is pre-populated with credential scopes prefixed by "offline_access" | Scope field contains "offline_access" followed by the credential scopes |
| 13 | Verify the scope placeholder text: "Enter OAuth scopes (space-separated)" | Placeholder text is correct when field is empty |
| 14 | Verify "Cancel" and "Authorize" buttons are present in the dialog | Both buttons are visible |
| 15 | Click "Cancel" to test cancellation | Dialog closes without taking any action |
| 16 | Click the "Login" button again | "Configuration OAuth" dialog reopens |
| **SUCCESSFUL OAUTH Phase** | | |
| 17 | Verify scopes are pre-populated correctly from the credential's Scopes field | Scope field is pre-filled |
| 18 | Click "Authorize" | Browser redirects to the Microsoft OAuth login page |
| 19 | Complete OAuth login with valid credentials on the provider page | OAuth provider grants authorization |
| 20 | Verify redirect back to the Elitea application after successful authorization | User is returned to the Elitea credential page |
| 21 | Verify a success indicator or toast message confirming OAuth token was obtained | Success toast or indicator is displayed |
| 22 | Verify the "Login" button changes to "Logout" | Button label is now "Logout" |
| 23 | Click "Test connection" | Connection test succeeds using the OAuth token |
| 24 | Verify Test connection shows success toast: "The connection is OK!" | Success toast is displayed |
| **PERSISTENCE & REUSE Phase** | | |
| 25 | Navigate away from the credential (e.g., go to Toolkits or Credentials list) | Navigation occurs successfully |
| 26 | Return to the same credential detail page | Credential page loads |
| 27 | Verify the OAuth token is still valid ("Logout" button is present) | Logout button is still displayed, indicating the token persists |
| 28 | Link this credential to a SharePoint toolkit | Credential is selected in the toolkit configuration |
| 29 | Verify toolkit operations work using the saved OAuth-authorized credential | Toolkit operation completes successfully |
| 30 | Verify no re-authorization prompt appears when reusing the credential in different contexts | No OAuth login prompt is triggered during reuse |
| **FAILED OAUTH Phase (Error Handling)** | | |
| 31 | Navigate back to the credential detail page | Credential detail page loads |
| 32 | Click the "Logout" button to clear the token | Token is cleared; button changes back to "Login" |
| 33 | Click the "Login" button | "Configuration OAuth" dialog opens |
| 34 | Modify scopes to include an invalid scope (e.g., "Invalid.Scope.xyz") | Scope field is updated with the invalid scope |
| 35 | Click "Authorize" | Browser redirects to the OAuth provider login page |
| 36 | Verify the OAuth provider shows an error or denies authorization | Provider displays an error or access denied message |
| 37 | Verify Elitea handles the failure gracefully (shows error message, does not crash) | Elitea displays an informative error message without crashing |
| 38 | Alternatively, click "Authorize" then cancel/close the OAuth provider login page | OAuth provider page is closed by the user |
| 39 | Verify Elitea shows an appropriate message about incomplete or cancelled authorization | Message about incomplete/cancelled authorization is displayed |

---

## Expected Final State

The complete OAuth lifecycle is validated: credential created with correct fields, OAuth modal shows pre-populated values, successful authorization results in Logout button and working Test connection, token persists across navigation and enables toolkit operations, and failed/cancelled OAuth flows are handled gracefully without crashes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Delegated auth fields appear correctly; OAuth modal is pre-populated; successful authorization changes Login to Logout; Test connection succeeds; token persists and enables toolkit operations; failed OAuth shows graceful error messages.

**Fail:**
- Any step produces an error or unexpected result.
- Delegated fields do not appear, OAuth modal is not pre-populated, Login does not change to Logout, Test connection fails after OAuth, token is lost after navigation, or failed OAuth causes a crash or unhandled error.

---

## Notes

**Source functional tests:** ELITEA-1981 (OAuth Required Flow), ELITEA-1982 (OAuth Modal), ELITEA-1983 (Successful OAuth), ELITEA-1984 (Failed OAuth), ELITEA-1985 (Saved Credential Reuse)

**Regression rationale:** Consolidates the complete OAuth journey into one comprehensive E2E scenario, covering both happy path (authorization success, token persistence, toolkit integration) and error handling (invalid scopes, cancellation). All critical checkpoints preserved: form fields for Delegated auth, Login button availability, modal pre-population, redirect and token storage, Login→Logout transition, Test connection validation, cross-navigation token persistence, toolkit integration without re-auth, and graceful error handling.

**Selected checkpoints:** Delegated auth fields visible; Login button present; OAuth modal pre-populated with server and scopes; Cancel closes modal; Authorize redirects to provider; successful login returns to Elitea; success toast displayed; Login→Logout button change; Test connection succeeds; token persists after navigation; toolkit operations work without re-auth; invalid scope triggers graceful error; cancelled OAuth shows informative message.
