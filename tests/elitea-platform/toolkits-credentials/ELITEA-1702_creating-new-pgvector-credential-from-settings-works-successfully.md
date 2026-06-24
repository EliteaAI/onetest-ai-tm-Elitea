---
id: ELITEA-1702
title: Verify creating a new PGVector credential from Settings works successfully
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has permissions to create integrations
- User has valid PGVector connection details

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Configuration Name | test-pgvector-config |
| Host | [valid test host] |
| Port | [valid test port] |
| Database | [valid test database] |
| Username | [valid test username] |
| Password | [valid test password] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | AI Configuration page loads |
| 2 | Click "+ New Integration" | Integration type selection opens |
| 3 | Select "PgVector" from the integration type list | PGVector configuration form loads with all required fields |
| 4 | Fill in Configuration Name: "test-pgvector-config" | Value is accepted |
| 5 | Fill in Host, Port, Database, Username, Password with valid test data | All values are accepted |
| 6 | Click "Save" or "Create" button | Loading indicator appears; form submits |
| 7 | Observe response | Success message/toast notification appears; new credential "test-pgvector-config" appears in AI Configuration list |

## Expected Final State

New PGVector credential is successfully created and appears in the AI Configuration list.

## Pass/Fail Criteria

**Pass:**
- PGVector form loads with all required fields
- All fields accept valid input
- Save button is enabled when fields are filled
- Form submits successfully
- Success message appears
- New credential appears in configuration list
- No JavaScript errors in console

**Fail:**
- Form fails to load or is missing fields
- Valid data is rejected
- Save fails with error
- No success message appears
- Credential doesn't appear in list
- JavaScript errors occur
