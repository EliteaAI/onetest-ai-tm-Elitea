---
id: ELITEA-1068
title: "GitHub App Credential Saves Successfully and Persists Correctly"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials, int:github, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3986]
---
# ELITEA-1068: GitHub App Credential Saves Successfully and Persists Correctly

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a GitHub App credential can be created and saved, and that the saved credential is listed and accessible after saving.

**Coverage:**
- Credential form accepts all required fields (App ID, Installation ID, Private Key)
- Credential is saved without error
- Saved credential appears in the Credentials list with the correct name
- Credential can be reopened and its non-sensitive fields (App ID, Installation ID, name) are retained

## Preconditions

- Logged in to {{base_url}}
- Valid GitHub App credentials (App ID, Installation ID, private key) are available

## Test Data

- Credential name: `test-github-app-3986`
- App ID: `<valid App ID>`
- Installation ID: `<valid Installation ID>`
- Private Key: Full PEM format

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials. Click '+ New Credential'. | New credential form opens. |
| 2 | Select GitHub App as the credential type. | GitHub App fields are displayed. |
| 3 | Enter credential name 'test-github-app-3986', valid App ID, Installation ID, and a full PEM private key. | All fields accept input without validation errors. |
| 4 | Click Save (or equivalent). | Credential is saved. No error is shown. A success notification or redirect occurs. |
| 5 | Locate 'test-github-app-3986' in the Credentials list. | The credential is listed with the name 'test-github-app-3986' and type 'GitHub App'. |
| 6 | Click on the credential to open it. | App ID and Installation ID are displayed correctly. Private Key field is masked or shows a placeholder. |

## Expected Final State

App ID and Installation ID are displayed correctly. Private Key field is masked or shows a placeholder.

## Pass/Fail Criteria

**Pass:**
- Credential saves without error
- Credential appears in the list with the correct name and type
- Non-sensitive fields are retained when reopening

**Fail:**
- Save fails with an error message
- Credential does not appear in the list after saving
- Fields are blank or incorrect when reopening the credential
