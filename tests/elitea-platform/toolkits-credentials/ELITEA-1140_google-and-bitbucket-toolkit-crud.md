---
id: ELITEA-1140
title: "Google and Bitbucket Toolkit CRUD"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateCredential.test_create_credential
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateToolkit.test_create_toolkit
  - tests.ui.toolkits.test_toolkit_parameterized.TestToolkitTestSettings.test_toolkit_test_settings
  - tests.ui.toolkits.test_toolkit_parameterized.TestChatWithToolkit.test_chat_with_toolkit
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1861
tags: []
requirements: []
---
# ELITEA-1140: Google and Bitbucket Toolkit CRUD

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that users can create and manage Google and Bitbucket toolkits with credentials, similar to GitHub toolkit (TC-0011, TC-0020).

**Coverage:**
- Create Google credentials
- Create Google toolkit using credentials
- Test Google toolkit settings
- Create Bitbucket credentials
- Create Bitbucket toolkit using credentials
- Test Bitbucket toolkit settings
- Delete toolkits and credentials

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Valid credentials for Google and/or Bitbucket services are available
- Browser: Chrome or Chromium
- Note: Bitbucket token may be expired — if so, skip Bitbucket tests

## Test Data

- URL: {{base_url}}
- Google credential display name: AutoTest Google
- Bitbucket credential display name: AutoTest Bitbucket
- Toolkit name pattern: AutoTest [Type] Toolkit
- Bitbucket settings: project key, repository name, branch master

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify your Google/Bitbucket credentials are still valid. If the Bitbucket token is expired (returns 401), skip the Bitbucket portion of this test. | Credentials are valid, or you have a clear reason to skip. |
| 2 | Navigate to Credentials from the sidebar. Click 'Create credential'. Select the toolkit type (e.g., Google or Bitbucket). Fill in the Display Name and authentication fields (tokens, URLs, etc.). | The form is filled out. The Save button becomes enabled. |
| 3 | Click Save. Wait for the page to navigate back to the Credentials list. | The page returns to the Credentials list. The new credential is visible. |
| 4 | Verify the credential appears in the Credentials list with the correct name. | The credential is found in the list with the matching display name. |
| 5 | Navigate to Toolkits from the sidebar. Click 'Create toolkit'. Select the same toolkit type. Fill in the name, description, select your credential from the dropdown, and fill any type-specific fields (repository, branch, etc.). | The form is filled with the credential selected. |
| 6 | Click Save. Wait for the page to navigate away from the create page. | The toolkit is created. The URL no longer shows '/create'. |
| 7 | Clean up: Delete the toolkit and credential you created. Go to each one's detail page, use the delete option, and confirm. | Both the toolkit and credential are deleted successfully. |

## Expected Final State

Both the toolkit and credential are deleted successfully.

## Pass/Fail Criteria

**Pass:**
- Credential pre-check passes (or test properly skips)
- Credential created via UI and visible in API
- Toolkit created with correct credential association
- Cleanup completes without errors

**Fail:**
- Credential creation fails or form validation errors
- Toolkit creation fails to associate credential
- Navigation doesn't complete after save
- Cleanup leaves orphaned entities
- Bitbucket token expired (expected skip, not failure)
