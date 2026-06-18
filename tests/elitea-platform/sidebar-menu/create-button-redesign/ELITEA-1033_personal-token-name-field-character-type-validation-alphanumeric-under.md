---
id: ELITEA-1033
title: "Personal Token Name Field: Character Type Validation (Alphanumeric, Underscore, Hyphen Only)"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5167, EliteaAI/elitea_issues#5135]
---
# ELITEA-1033: Personal Token Name Field: Character Type Validation (Alphanumeric, Underscore, Hyphen Only)

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Personal Token name field only accepts alphanumeric characters, underscores (`_`), and hyphens (`-`), and rejects all other characters.

**Coverage:**
- Acceptance of valid characters (alphanumeric, `_`, `-`)
- Rejection of special characters (spaces, `@`, `!`, `/`)

## Preconditions

- Logged in to ELITEA with access to Settings > Personal Tokens

## Test Data

| Input | Expected Result |
|---|---|
| `my_token-01` | Accepted |
| `MyToken123` | Accepted |
| `token@name` | Rejected |
| `token name` (space) | Rejected |
| `token!` | Rejected |
| `token/name` | Rejected |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Personal Tokens; click `+ Token`; enter `my_token-01` in the Name field; submit | Token is created successfully |
| 2 | Create new token; enter `token@name`; attempt submit | Validation error appears; token is NOT created |
| 3 | Enter `token name` (with space) in the Name field | Validation error appears |
| 4 | Enter `token!` in the Name field | Validation error appears |
| 5 | Enter `token/name` in the Name field | Validation error appears |

## Expected Final State

Validation error appears

## Pass/Fail Criteria

**Pass:**
- Valid names (alphanumeric, `_`, `-`) are accepted
- Invalid characters trigger a validation error and block creation

**Fail:**
- Token is created with invalid characters in the name
- No error shown for invalid character input
