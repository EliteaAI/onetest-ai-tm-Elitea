---
id: ELITEA-1710
title: Verify PGVector configuration form displays all required fields correctly
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
- User has permissions to create integrations
- User is on Settings → AI Configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | Page loads |
| 2 | Click "+ New Integration" | Integration type selection opens |
| 3 | Select "PgVector" from integration types | PGVector configuration form loads |
| 4 | Observe the PGVector configuration form | Form displays all required fields: Configuration Name, Host, Port, Database, Username, Password; field labels are clear; required fields marked with asterisk (*); placeholder text appears if applicable; field types are appropriate |

## Expected Final State

PGVector configuration form is complete with all required fields properly labeled and formatted.

## Pass/Fail Criteria

**Pass:**
- Form loads completely without errors
- All required fields present: Configuration Name, Host, Port, Database, Username, Password
- Field labels are clear and descriptive
- Required fields marked with asterisk (*)
- Placeholder text appears in empty fields if applicable
- Field types are appropriate (text, number, password)
- Form layout is clean and organized

**Fail:**
- Form fails to load or is incomplete
- Required fields are missing
- Labels are unclear or missing
- Required field indicators missing
- Field types are incorrect
- Form layout is broken
