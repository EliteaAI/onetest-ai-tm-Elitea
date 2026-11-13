---
id: ELITEA-1140
title: "Jira and Confluence Toolkit CRUD"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateCredential.test_create_credential[jira]
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateToolkit.test_create_toolkit[jira]
  - tests.ui.toolkits.test_toolkit_parameterized.TestToolkitTestSettings.test_toolkit_test_settings[jira]
  - tests.ui.toolkits.test_toolkit_parameterized.TestChatWithToolkit.test_chat_with_toolkit[jira]
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateCredential.test_create_credential[confluence]
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateToolkit.test_create_toolkit[confluence]
  - tests.ui.toolkits.test_toolkit_parameterized.TestToolkitTestSettings.test_toolkit_test_settings[confluence]
  - tests.ui.toolkits.test_toolkit_parameterized.TestChatWithToolkit.test_chat_with_toolkit[confluence]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2364
tags: []
requirements: []
---
# ELITEA-1140: Jira and Confluence Toolkit CRUD

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that users can create and manage Jira and Confluence toolkits with credentials, similar to GitHub toolkit (TC-0011, TC-0020).

**Coverage:**
- Create Jira credentials
- Create Jira toolkit using credentials
- Test Jira toolkit settings
- Execute a Jira toolkit tool from Chat
- Create Confluence credentials
- Create Confluence toolkit using credentials
- Test Confluence toolkit settings
- Execute a Confluence toolkit tool from Chat
- Delete toolkits and credentials

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Valid credentials for Jira and/or Confluence services are available
- Browser: Chrome or Chromium
- Note: Confluence token may be expired — if so, skip Confluence tests

## Test Data

- URL: {{base_url}}
- Jira credential display name: AutoTest Jira
- Confluence credential display name: AutoTest Confluence
- Toolkit name pattern: AutoTest [Type] <timestamp> — at most 32 characters (the Toolkit Name field caps input at 32)
- Jira/Confluence settings: base URL, username, API token
- Confluence toolkit field: Space Key
- Test tool — Jira: *List projects* (`list_projects`); Confluence: *List pages* (`list_pages_with_label`, label `test`)
- Chat message — Jira: `List all Jira projects`; Confluence: `Use the list_pages_with_label tool to list pages with label 'test' in Confluence`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify your Jira/Confluence credentials are still valid. If the Confluence token is expired (returns 401), skip the Confluence portion of this test. | Credentials are valid, or you have a clear reason to skip. |
| 2 | Navigate to Credentials from the sidebar. Click 'Create credential'. Select the toolkit type (e.g., Jira or Confluence). Fill in the Display Name and authentication fields (tokens, URLs, etc.). | The form is filled out. The Save button becomes enabled. |
| 3 | Click Save. Wait for the page to navigate back to the Credentials list. | The page returns to the Credentials list. The new credential is visible. |
| 4 | Verify the credential appears in the Credentials list with the correct name. | The credential is found in the list with the matching display name. |
| 5 | Navigate to Toolkits from the sidebar. Click 'Create toolkit'. Select the same toolkit type. Fill in the name, description, select your credential from the dropdown, and fill any type-specific fields (repository, branch, etc.). | The form is filled with the credential selected. |
| 6 | Click Save. Wait for the page to navigate away from the create page. | The toolkit is created. The URL no longer shows '/create'. |
| 7 | On the toolkit detail page, click the **Test** button in the header action bar. | The Test Toolkit page opens at `/toolkits/all/{id}/test` with a *Test Settings* column showing the tool-selection empty state. |
| 8 | Open the **Tool** select, choose the test tool (Jira: *List projects*; Confluence: *List pages*, fill parameter `label` = `test`), then click **Run Test**. | The Test Settings panel shows the chosen tool; the tool runs with the linked credential and the Results column shows a successful result (Jira: `list_projects` with projects; Confluence: `list_pages_with_label` with pages) — no *Error debugging info*. |
| 9 | Open Chat in a new conversation, add the toolkit as a participant (**+** → **Toolkits**), and send the chat message from Test Data. | The toolkit's tool (Jira: `list_projects`; Confluence: `list_pages_with_label`) is called once and returns its result successfully; a new AI response appears describing it (Jira projects / Confluence pages). |
| 10 | Clean up: Delete the toolkit and credential you created. Go to each one's detail page, use the delete option, and confirm. | Both the toolkit and credential are deleted successfully. |

## Expected Final State

Both the toolkit and credential are deleted successfully.

## Pass/Fail Criteria

**Pass:**
- Credential pre-check passes (or test properly skips)
- Credential created via UI and visible in API
- Toolkit created with correct credential association
- Test Toolkit run returns a successful tool result
- Toolkit tool executes successfully from Chat and the response reflects its result
- Cleanup completes without errors

**Fail:**
- Credential creation fails or form validation errors
- Toolkit creation fails to associate credential
- Navigation doesn't complete after save
- Test Toolkit run shows an error with valid credentials
- Chat response does not invoke the tool, or the tool call fails
- Cleanup leaves orphaned entities
- Confluence token expired (expected skip, not failure)
