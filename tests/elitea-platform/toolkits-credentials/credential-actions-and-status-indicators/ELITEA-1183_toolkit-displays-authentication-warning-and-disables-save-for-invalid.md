---
id: ELITEA-1183
title: "Toolkit displays authentication warning and disables Save for invalid credentials"
priority: high
type: functional
module: credential-actions-and-status-indicators
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_toolkit_indicators_for_credentials.TestToolkitCredentialIndicators.test_toolkit_credential_indicators_e2e
tags: []
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/2359"
requirements: [EliteaAI/elitea_issues#4906, EliteaAI/elitea_issues#5114]
---
# ELITEA-1183: Toolkit displays authentication warning and disables Save for invalid credentials

**Module:** Credential Actions And Status Indicators · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a Jira or GitHub toolkit is configured with invalid credentials, the system displays an authentication warning explaining why the Save button is disabled.

**Coverage:**
- Warning message appears starting with "Authentication failed:" in the toolkit configuration section
- Save button is disabled while authentication fails
- User can understand why Save is unavailable
- Behavior verified for both Jira and GitHub toolkit types

## Preconditions

- User is logged into Elitea platform ({{base_url}})
- User has permissions to create credentials and toolkits
- Jira and GitHub integrations are available in the system

## Test Data

| Field | Value |
|---|---|
| Jira credential display name | InvalidJira_Test |
| Jira Bearer token | 1231414Htr3434hR (invalid) |
| Jira Base URL | https://jiraeu.epam.com |
| Jira toolkit name | InvalidJira_Toolkit_Test |
| GitHub credential display name | InvalidGitHub_Test |
| GitHub token | ghp_invalidtoken123456789012345678901234 (invalid) |
| GitHub toolkit name | InvalidGitHub_Toolkit_Test |
| Toolkit description | Test toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials from sidebar. Click + Credential. | Credential creation form is displayed. |
| 2 | Select Jira as the credential type. | Jira credential form is displayed. |
| 3 | Fill in: Display Name = InvalidJira_Test, Bearer token = 1231414Htr3434hR, Base URL = https://jiraeu.epam.com. | All fields are filled with provided values. |
| 4 | Click Save. | Credential is created successfully and appears in the credentials list. |
| 5 | Navigate to Toolkits from sidebar. Click + Toolkit. | Toolkit creation form is displayed. |
| 6 | Select Jira as the toolkit type. | Jira toolkit form is displayed. |
| 7 | Fill in: Toolkit Name = InvalidJira_Toolkit_Test, Description = Test toolkit, Jira Configuration = select credential InvalidJira_Test from step 4. | All fields are filled. |
| 8 | Click Save. | Toolkit is created and user is redirected to the toolkit detail page. |
| 9 | Observe the Jira Configuration section on the toolkit detail page. | Warning message is visible starting with "Authentication failed:" (e.g., "Authentication failed: Invalid bearer token"). |
| 10 | Observe the Jira Configuration row, then open the Jira Configuration dropdown and locate the selected credential's option. | The configuration row is flagged as invalid (warning underline on the field). In the open dropdown, the selected credential's option shows a distinct Warning/Error icon/badge (separate from the warning text banner under the field). |
| 11 | Inspect the Warning/Error icon on the credential's option (hover shows its tooltip; the warning banner under the field carries the same tooltip). Close the dropdown. | A tooltip appears. Tooltip text describes the error state (e.g., "Authentication failed: …"). Tooltip is not blank. |
| 12 | Check the Save button state. | Save button is disabled while the authentication warning and icon are shown. |

## Expected Final State

Save button is disabled while the authentication warning and icon are shown.

## Pass/Fail Criteria

**Pass:**
- Authentication warning message is visible for both Jira and GitHub toolkit configurations
- Warning message starts with "Authentication failed:"
- Warning/Error icon is visible and distinct from the text message
- Tooltip on the Warning/Error icon is present and contains meaningful text
- Save button is disabled while warning is shown
- User can clearly understand why Save is unavailable

**Fail:**
- No warning message is displayed (regression of bug EliteaAI/elitea_issues#4906)
- Warning message does not start with "Authentication failed:"
- Warning/Error icon is absent
- Tooltip on the icon is blank or missing
- Save button is enabled despite invalid credentials
- Page crashes or shows unhandled error
