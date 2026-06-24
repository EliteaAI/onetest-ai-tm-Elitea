---
id: ELITEA-1712
title: Verify "Save" button functionality when creating new PGVector credentials
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on PGVector configuration creation form
- User has valid test data ready

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Configuration Name | test-save-pgvector |
| Host | [valid test host] |
| Port | [valid test port] |
| Database | [valid test database] |
| Username | [valid test username] |
| Password | [valid test password] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration → New Integration → PgVector | Form loads |
| 2 | Observe "Save" button state with empty fields | Save button is disabled |
| 3 | Fill in all required fields with valid data | Fields accept input |
| 4 | Observe "Save" button state | Save button becomes enabled |
| 5 | Click "Save" button | Loading indicator appears; form submits |
| 6 | Wait for response | Success message/toast appears; user is redirected to AI Configuration list OR form closes |
| 7 | Check AI Configuration list | New credential "test-save-pgvector" appears in the list |

## Expected Final State

Save button correctly enables/disables based on form validation and successfully saves the credential.

## Pass/Fail Criteria

**Pass:**
- Save button is disabled when fields are empty
- Save button enables when all required fields are filled
- Clicking Save triggers form submission
- Loading indicator appears during processing
- Success message appears on success
- User is redirected or form closes after save
- New credential appears in configuration list
- No JavaScript errors in console

**Fail:**
- Save button state is incorrect
- Form doesn't submit on save
- No loading indicator
- No success message
- Credential doesn't appear in list
- JavaScript errors occur
