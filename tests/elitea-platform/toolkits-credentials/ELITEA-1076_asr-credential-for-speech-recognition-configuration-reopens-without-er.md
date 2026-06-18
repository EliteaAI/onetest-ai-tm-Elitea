---
id: ELITEA-1076
title: "ASR Credential for Speech Recognition — Configuration Reopens Without Error"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials, feat:settings, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4888]
---
# ELITEA-1076: ASR Credential for Speech Recognition — Configuration Reopens Without Error

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after creating an ASR credential for speech recognition and saving it, reopening the configuration displays the credential form correctly without raw JSON or "Toolkit must have settings field" errors.

**Coverage:**
- ACR credential creation for speech recognition type
- Configuration persistence after save
- Reopening the saved configuration renders the form correctly
- No raw JSON error displayed on reopen

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has access to a project with permissions to manage credentials
- No existing ASR speech recognition credential in the project

## Test Data

- Credential type: ASR (speech recognition)
- Credential name: test-acr-speech-cred
- Any valid ASR credential values

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the project Configuration page. | Configuration page loads without errors. |
| 2 | Open the Credentials section and click to add a new credential. Select type 'ASR' for speech recognition. | ASR credential creation form is displayed with all required fields. |
| 3 | Fill in all required fields with valid ASR credential values (name: test-acr-speech-cred). Click Save. | Credential is saved successfully. A success confirmation is shown. |
| 4 | Close or navigate away from the credential configuration, then click on the newly created ACR credential to reopen it. | The ASR credential configuration form reopens correctly, displaying the saved values. No raw JSON is shown. No 'Toolkit must have settings field' error is displayed. |

## Expected Final State

The ASR credential configuration form reopens correctly, displaying the saved values. No raw JSON is shown. No 'Toolkit must have settings field' error is displayed.

## Pass/Fail Criteria

**Pass:**
- ASR credential is created and saved without errors
- Reopening the credential configuration renders the form with saved data
- No raw JSON block appears anywhere on the page
- No "Toolkit must have settings field" error message is shown

**Fail:**
- Reopening the credential configuration displays raw JSON
- "Toolkit must have settings field" error message appears on reopen
- The configuration form fails to render after saving
