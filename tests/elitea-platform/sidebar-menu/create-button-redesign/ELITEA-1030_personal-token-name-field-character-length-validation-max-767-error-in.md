---
id: ELITEA-1030
title: "Personal Token Name Field: Character Length Validation (Max 767, Error Includes 768)"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5167, EliteaAI/elitea_issues#5135]
---
# ELITEA-1030: Personal Token Name Field: Character Length Validation (Max 767, Error Includes 768)

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Personal Token name field enforces a maximum length of 767 characters, shows an error on exceeding this limit, and that the error message includes the limit number (768).

**Coverage:**
- Acceptance of 767-character names
- Rejection of 768+ character names
- Error message content with character limit

## Preconditions

- Logged in to ELITEA with access to Settings > Personal Tokens
- Sidebar in expanded state

## Test Data

- Valid name: 'a' \u00d7 767 characters
- Invalid name: 'a' \u00d7 768 characters
- Invalid name: 'a' \u00d7 1000 characters

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Personal Tokens; click `+ Token` | Token creation form opens |
| 2 | Enter a 767-character alphanumeric string in the Name field (e.g., 'a' × 767) | Input is accepted; no validation error shown |
| 3 | Clear the field; enter a 768-character string (e.g., 'a' × 768) | Validation error appears |
| 4 | Inspect the error message text | Error message explicitly includes '768' as the maximum limit |
| 5 | Attempt to submit the form with the 768-char name | Form submission is blocked; error persists |
| 6 | Clear and enter a 1000-character string | Same validation error appears |

## Expected Final State

Same validation error appears

## Pass/Fail Criteria

**Pass:**
- 767-char name is accepted without error
- 768+ char name triggers a clear error message that includes \"768\"
- Form submission is blocked when the limit is exceeded

**Fail:**
- 768+ char name is accepted and token is created
- Error message does not mention the maximum character count
- Validation fires only on submit with no real-time feedback (note if observed)
