---
id: ELITEA-1141
title: "GitHub Toolkit and Credentials"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateCredential.test_create_credential[github]
  - tests.ui.toolkits.test_toolkit_parameterized.TestCreateToolkit.test_create_toolkit[github]
  - tests.ui.toolkits.test_toolkit_parameterized.TestToolkitTestSettings.test_toolkit_test_settings[github]
  - tests.ui.toolkits.test_toolkit_parameterized.TestChatWithToolkit.test_chat_with_toolkit[github]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2363
tags: []
requirements: []
---
# ELITEA-1141: GitHub Toolkit and Credentials

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can create GitHub credentials, create a toolkit using those credentials, test the toolkit settings, and execute a toolkit tool from Chat.

## Preconditions

- User logged into Elitea
- Valid GitHub token available
- Access to Credentials, Toolkits and Chat sections

## Test Data

- URL: {{base_url}}
- Credential type: GitHub (Base URL `https://api.github.com`, pre-filled)
- Test token: (from .env.test)
- Repository: a repository the token can read (e.g. `EliteaAI/elitea-testing`)
- Test tool: *List branches* (`list_branches_in_repo`)
- Chat message: `List branches in the repository`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials, create a GitHub credential: fill Display Name and Access Token, click **Save** | The page returns to the Credentials list (`/credentials/all`); the credential is visible in the list with its Display Name |
| 2 | Navigate to Toolkits, click **Create toolkit** and choose the **GitHub** type card | The GitHub toolkit form opens with a credential (GitHub configuration) selector |
| 3 | Fill Toolkit Name and Description, select the credential from step 1, fill **Repository**, click **Save** | The page leaves the create form; the toolkit is saved and linked to the selected credential |
| 4 | On the toolkit detail page, click the **Test** button in the header action bar | The Test Toolkit page opens at `/toolkits/all/{id}/test` (breadcrumb `Toolkits & Indexes / <toolkit> / Test Toolkit`) with a *Test Settings* column showing the tool-selection empty state and a *Results* column |
| 5 | In the Test Settings empty state open the **Tool** select and choose a tool (e.g. *List branches*), then click **Run Test** | The Test Settings panel shows the chosen tool, model selector and parameters; the tool runs with the linked credential and the Results column shows a successful tool result (`list_branches_in_repo`, output lists the branches, e.g. `main`) — no *Error debugging info* |
| 6 | Open Chat in a new conversation, add the GitHub toolkit as a participant (**+** → **Toolkits**), send `List branches in the repository` | The toolkit's `list_branches_in_repo` tool is called once and returns the repository's branch list; a new AI response appears describing the repository's branches |

## Expected Final State

Connection test passes, and the toolkit executes its tool successfully from Chat.

## Pass/Fail Criteria

**Pass:**
- Credential created successfully and visible in the Credentials list
- Toolkit created and linked to the credential
- Test settings validates connection
- Toolkit tool executes successfully from Chat and the response reflects its result

**Fail:**
- Credential creation fails
- Toolkit not linked to credential
- Test fails with valid token
- Chat response does not invoke the tool, or the tool call fails

## Cleanup

- Delete the toolkit and the credential created by this case
