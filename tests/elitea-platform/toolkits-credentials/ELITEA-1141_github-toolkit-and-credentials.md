---
id: ELITEA-1141
title: "GitHub Toolkit and Credentials"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_github_toolkit.test_create_github_credential
  - tests.ui.toolkits.test_github_toolkit.test_create_github_toolkit
  - tests.ui.toolkits.test_github_toolkit.test_github_toolkit_test_settings
  - tests.ui.toolkits.test_github_toolkit.test_chat_with_github_toolkit
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
| ? | Click Test Settings | Connection test passes |

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
