---
id: ELITEA-1005
title: "Sensitive Parameter Masking in Authorization Dialog [Parametrized]"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1005: Sensitive Parameter Masking in Authorization Dialog [Parametrized]

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that parameter values with sensitive field names (password, token, access_token, api_key, secret, client_secret) are masked as *** in the dialog, while non-sensitive parameter values are shown in full. [Parametrized]

## Preconditions

- A sensitive tool is configured that passes parameters including sensitive fields
- Authorization dialog is visible

## Test Data

Sensitive field names (masked): password, token, access_token, api_key, secret, client_secret
Non-sensitive field names (full value): repository (e.g., elitea/backend-api), title (e.g., feat: Add auth), branch (e.g., main)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger a sensitive tool that includes parameters with sensitive field names (password, token, access_token, api_key, secret, client_secret) and non-sensitive field names (repository, title, branch). | Authorization dialog appears with the Parameters section expanded. |
| 2 | For each parameter with a sensitive field name (password, token, access_token, api_key, secret, client_secret) — observe the displayed value. | Each value is masked and displayed as ***. The parameter key name is still visible. |
| 3 | For each non-sensitive parameter (repository, title, branch) — observe the displayed value. | Values are displayed in full, unmasked. |
| 4 | Click [Authorize] and confirm the tool receives the original unmasked values (verify by checking the actual side effect — e.g., tool used the correct token). | Tool executes using the actual sensitive parameter values, not the masked display values. |

## Expected Final State

Tool executes using the actual sensitive parameter values, not the masked display values.

## Pass/Fail Criteria

Pass:
- All 6 sensitive field names have their values masked as ***
- Parameter key names remain visible even when value is masked
- All non-sensitive parameters show full values
- Tool receives correct unmasked values after Authorize

Fail:
- Any sensitive parameter value is shown in plain text
- Non-sensitive parameter values are incorrectly masked
- Tool receives *** as the actual value after Authorize (masking affecting execution)
