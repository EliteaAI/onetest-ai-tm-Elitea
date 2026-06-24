---
id: ELITEA-1711
title: Verify validation works when creating PGVector credentials with missing/invalid data
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1711: Verify validation works when creating PGVector credentials with missing/invalid data

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that form validation works correctly when creating PGVector credentials, rejecting empty required fields and invalid input formats with clear error messages.


## Preconditions

- User is logged in to `{{base_url}}`
- User is on PGVector configuration creation form (Settings → AI Configuration → New Integration → PgVector)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Invalid Port | abc |
| Invalid Host | @#$% |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Leave all fields empty, click "Save" | Validation errors appear for all required fields |
| 2 | Fill only "Configuration Name", leave others empty, click "Save" | Validation errors appear for remaining required fields |
| 3 | Enter invalid Port: "abc" (non-numeric) | Error message: "Port must be numeric" |
| 4 | Enter invalid Host with special characters only: "@#$%" | Error message appears for invalid host format |
| 5 | Enter valid data for all fields EXCEPT Password, click "Save" | Validation error appears for Password field |
| 6 | Attempt to save with duplicate configuration name (if validation exists) | Error message appears for duplicate name |

## Expected Final State

Form validation prevents submission of invalid or incomplete data with clear error messages.

## Pass/Fail Criteria

**Pass:**
- Empty required fields show validation errors
- Each field shows specific error message
- Invalid port number shows error
- Save button remains disabled OR shows error on submit when validation fails
- Form does not submit with validation errors
- Error messages are clear and actionable
- Red borders/indicators appear around invalid fields
- After fixing errors, validation passes

**Fail:**
- Form submits with invalid data
- No validation errors appear
- Error messages are unclear
- Visual indicators are missing
- Validation is inconsistent

**Blocked** 
Test connection is not yet implemented for this test case
