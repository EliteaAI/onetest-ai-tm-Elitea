---
id: ELITEA-1700
title: Verify PGVector configuration creation is accessible via Settings → AI Configuration → New Integration
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1700: Verify PGVector configuration creation is accessible via Settings → AI Configuration → New Integration

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that PGVector credential creation functionality remains accessible through the Settings → AI Configuration → New Integration path after removal from toolkit dropdown.


## Preconditions

- User is logged in to `{{base_url}}`
- User has admin/appropriate permissions to create integrations
- User has access to Settings

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click on "Settings" in the left navigation menu | Settings page loads successfully |
| 2 | Click on "AI Configuration" in the Settings menu | AI Configuration page loads |
| 3 | Click "+ New Integration" button or equivalent | Integration type selection screen opens |
| 4 | Observe the "Select the integration Type" screen | Multiple integration options are displayed |
| 5 | Look for "PgVector" in the available integration types | "PgVector" appears in the integration type list |
| 6 | Verify PgVector option is clickable | PgVector option is enabled and interactive |

## Expected Final State

PGVector integration type is accessible and selectable from Settings → AI Configuration → New Integration path.

## Pass/Fail Criteria

**Pass:**
- Settings → AI Configuration path is accessible
- "New Integration" button is visible and enabled
- Integration type selection screen displays
- "PgVector" appears in the list with appropriate icon
- PgVector option is clickable

**Fail:**
- Settings or AI Configuration page is inaccessible
- "New Integration" button is missing or disabled
- PgVector is missing from integration type list
- PgVector option is not clickable
