---
id: ELITEA-1066
title: "Test Connection Succeeds for All GitHub App Private Key Format Variants [Parametrized]"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials, int:github, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3986]
---
# ELITEA-1066: Test Connection Succeeds for All GitHub App Private Key Format Variants [Parametrized]

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Test Connection" button returns a success confirmation for a valid GitHub App private key regardless of whether the `-----BEGIN RSA PRIVATE KEY-----` and `-----END RSA PRIVATE KEY-----` lines are present, absent, or partially present.

**Coverage:**
- Test Connection succeeds with full PEM (BEGIN + END present)
- Test Connection succeeds with BEGIN header only (no END footer)
- Test Connection succeeds with END footer only (no BEGIN header)
- Test Connection succeeds with raw key body (no BEGIN or END lines)

## Preconditions

- Logged in to {{base_url}}
- A valid GitHub App private key (.pem file) is available
- App ID and Installation ID are known

## Test Data

| Variant | Private Key Format |
|---|---|
| Full PEM | `-----BEGIN RSA PRIVATE KEY-----
<key body>
-----END RSA PRIVATE KEY-----` |
| Header only | `-----BEGIN RSA PRIVATE KEY-----
<key body>` |
| Footer only | `<key body>
-----END RSA PRIVATE KEY-----` |
| Raw key | `<key body>` (no header or footer) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials in the Elitea project. Click '+ New Credential'. | New credential form opens. |
| 2 | Select GitHub App as the credential type. | GitHub App fields are displayed (App ID, Installation ID, Private Key). |
| 3 | Enter the valid App ID and Installation ID. | Fields accept input. |
| 4 | Paste the Full PEM variant private key into the Private Key field. | Key is accepted. |
| 5 | Click 'Test Connection'. | A success/confirmation message is displayed. No error message appears. |
| 6 | Clear the Private Key field. Paste the Header only variant. Click 'Test Connection'. | A success/confirmation message is displayed. No error message appears. |
| 7 | Clear the Private Key field. Paste the Footer only variant. Click 'Test Connection'. | A success/confirmation message is displayed. No error message appears. |
| 8 | Clear the Private Key field. Paste the Raw key variant (no header/footer). Click 'Test Connection'. | A success/confirmation message is displayed. No error message appears. |

## Expected Final State

A success/confirmation message is displayed. No error message appears.

## Pass/Fail Criteria

**Pass:**
- All four variants result in a success/confirmation message after clicking "Test Connection"
- No error message is shown for any valid key format variant

**Fail:**
- Any valid key format variant produces an error message on "Test Connection"
- "Test Connection" button is unresponsive for any variant
