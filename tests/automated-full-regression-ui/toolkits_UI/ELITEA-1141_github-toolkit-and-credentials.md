---
id: ELITEA-1141
title: "GitHub Toolkit and Credentials"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_github_toolkit.TestCreateGitHubCredential.test_create_github_credential
  - tests.ui.toolkits.test_github_toolkit.TestCreateGitHubToolkit.test_create_github_toolkit
  - tests.ui.toolkits.test_github_toolkit.TestGitHubToolkitTestSettings.test_github_toolkit_test_settings
  - tests.ui.toolkits.test_github_toolkit.TestChatWithGitHubToolkit.test_chat_with_github_toolkit
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

**Objective:** Verify that users can create GitHub credentials, create toolkits using those credentials, and test toolkit settings.

## Preconditions

- User logged into Elitea
- Valid GitHub token available
- Access to Credentials/Toolkits sections

## Test Data

- URL: {{base_url}}
- Credential type: GitHub
- Test token: (from .env.test)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Navigate to Credentials, create GitHub credential | Credential created, visible in list |
| ? | Navigate to Toolkits, create GitHub toolkit | Toolkit created with credential selector |
| ? | Select credential, configure toolkit | Toolkit linked to credential |
| ? | On the toolkit detail page, click the **Test** button in the header action bar | The Test Toolkit page opens at `/toolkits/all/{id}/test` (breadcrumb `Toolkits & Indexes / <toolkit> / Test Toolkit`) with a *Test Settings* column showing the tool-selection empty state and a *Results* column |
| ? | In the Test Settings empty state open the **Tool** select and choose a tool (e.g. *List branches*), then click **Run Test** | The Test Settings panel shows the chosen tool, model selector and parameters; the tool runs with the linked credential and the Results column shows a successful tool result (connection test passes) |

## Expected Final State

Connection test passes

## Pass/Fail Criteria

**Pass:**
- Credential created successfully
- Toolkit created with credential
- Test settings validates connection

**Fail:**
- Credential creation fails
- Toolkit not linked to credential
- Test fails with valid token
