---
id: ELITEA-1185
title: "Toolkit with missing credential — error state visible in Agent configuration with correct message format"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1185: Toolkit with missing credential — error state visible in Agent configuration with correct message format

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a toolkit referencing an unavailable credential is used in an Agent, the Agent's toolkit section displays an error that includes the credential title and project context in the expected format.

**Coverage:**
- Error banner is shown inline under the affected toolkit card in Agent configuration
- Error contains the credential title, project_id, and public_project_id reference
- Error format matches: `Value error, Configuration with title 'X' not found for project_id N or shared in public_project_id M`
- Toolkit name and "Show tools" link remain visible despite the error
- No sensitive credential data appears in the error

## Preconditions

- Logged in to {{base_url}} as User B
- A shared Agent exists in the project that includes a toolkit (e.g., GitHub, ADO) whose credential was created in a different project and is not available to User B
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Agent with broken toolkit: e.g., Agent using `test multy` toolkit referencing `sams_test-cred`
- Expected error pattern: `Value error, Configuration with title 'sams_test-cred' not found for project_id 13 or shared in public_project_id 1`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Agents and open the shared Agent that contains a toolkit with a missing credential. | Agent configuration page opens. |
| 2 | Scroll to the TOOLKITS section. Locate the toolkit card with a warning icon (⚠). | Toolkit card is visible with a warning icon. |
| 3 | Observe the error banner shown below the toolkit card. | An inline error banner is displayed containing the credential title (e.g., `sams_test-cred`), the project_id, and the public_project_id in the format: `Value error, Configuration with title 'X' not found for project_id N or shared in public_project_id M`. |
| 4 | Verify the toolkit name and 'Show tools' link are still visible. | Toolkit name and 'Show tools' link are rendered despite the error. |
| 5 | Inspect the error message for sensitive data. | No tokens, secrets, or passwords appear — only the credential title and project references. |

## Expected Final State

No tokens, secrets, or passwords appear — only the credential title and project references.

## Pass/Fail Criteria

**Pass:**
- Error banner appears inline under the affected toolkit card
- Error message contains the credential title, project_id, and public_project_id
- Toolkit name and Show tools link remain visible
- No sensitive credential data is exposed

**Fail:**
- No error is shown in the Agent's toolkit section
- Error message does not include the credential name or project reference
- Toolkit card is completely hidden or broken with no explanation
