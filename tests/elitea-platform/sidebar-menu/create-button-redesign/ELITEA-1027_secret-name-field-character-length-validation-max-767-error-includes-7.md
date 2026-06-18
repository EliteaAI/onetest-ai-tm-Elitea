---
id: ELITEA-1027
title: "Secret Name Field: Character Length Validation (Max 767, Error Includes 768)"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5167, EliteaAI/elitea_issues#5135]
---
# ELITEA-1027: Secret Name Field: Character Length Validation (Max 767, Error Includes 768)

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Secret name field enforces a maximum length of 767 characters, and that the error message on exceeding the limit explicitly includes \"768\".

**Coverage:**
- Acceptance of 767-char names
- Rejection of 768+ char names with correct error message

## Preconditions

- Logged in to ELITEA with access to Settings > Secrets

## Test Data

- Valid name: 'a' \u00d7 767 characters
- Invalid name: 'a' \u00d7 768 characters

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Secrets; click `+ Secret` | Secret creation form opens |
| 2 | Enter a 767-character alphanumeric string in the Name field | Input is accepted; no validation error |
| 3 | Clear the field; enter a 768-character string | Validation error appears |
| 4 | Inspect the error message | Error message includes the number '768' as the maximum |
| 5 | Attempt to submit with 768-char name | Form submission is blocked |

## Expected Final State

Form submission is blocked

## Pass/Fail Criteria

**Pass:**
- 767-char name accepted without error
- 768+ char name blocked with error message that includes \"768\"

**Fail:**
- Secret created with 768+ char name
- Error message does not include the character limit number
