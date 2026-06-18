---
id: ELITEA-1067
title: "Test Connection Returns an Error for Invalid GitHub App Credentials"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials, int:github, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3986]
---
# ELITEA-1067: Test Connection Returns an Error for Invalid GitHub App Credentials

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Test Connection" button correctly returns an error message when the provided GitHub App credentials are invalid — confirming that the validation logic is functional and does not produce false positives.

**Coverage:**
- Invalid App ID produces an error on Test Connection
- Invalid Installation ID produces an error on Test Connection
- Malformed / random private key produces an error on Test Connection

## Preconditions

- Logged in to {{base_url}}

## Test Data

| Variant | Invalid Input |
|---|---|
| Wrong App ID | `App ID = 000000` (non-existent), valid Installation ID and valid private key |
| Wrong Installation ID | Valid App ID, `Installation ID = 000000` (non-existent), valid private key |
| Bad private key | Valid App ID and Installation ID, `Private Key = "this-is-not-a-real-key"` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials. Click '+ New Credential'. Select GitHub App. | GitHub App credential form opens. |
| 2 | Enter App ID = 000000, a valid Installation ID, and a valid private key. Click 'Test Connection'. | An error message is displayed. No false-positive success message appears. |
| 3 | Update the App ID to a valid value. Set Installation ID = 000000. Keep the valid private key. Click 'Test Connection'. | An error message is displayed. |
| 4 | Restore a valid Installation ID. Replace the Private Key with 'this-is-not-a-real-key'. Click 'Test Connection'. | An error message is displayed. |

## Expected Final State

An error message is displayed.

## Pass/Fail Criteria

**Pass:**
- All three invalid input variants produce an error message on "Test Connection"
- No false-positive success messages are shown

**Fail:**
- Any invalid input variant results in a success message
- "Test Connection" shows no response (neither success nor error) for any variant
