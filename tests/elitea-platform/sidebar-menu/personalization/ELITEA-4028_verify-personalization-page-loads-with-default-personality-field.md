---
id: ELITEA-4028
title: "Verify Personalization page loads with Default Personality field"
priority: critical
type: functional
module: personalization
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-4028: Verify Personalization page loads with Default Personality field

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Personalization page loads correctly and displays the Default Personality field with proper UI elements

## Preconditions

- User is logged in to `{{base_url}}`
- User has valid account credentials

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test User | {{test_user_email}} |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings from sidebar | Settings page opens |
| 2 | Click on "Personalization" menu item | Personalization page loads successfully |
| 3 | Verify page header shows "Personalization" | Page header is visible |
| 4 | Verify user profile section at top (avatar, email) | User profile displays correctly |
| 5 | Locate "GENERAL" section | GENERAL section is visible and expanded by default |
| 6 | Verify "Default Personality" field exists with info icon (ℹ️) | Field is present with label and info icon |

## Expected Final State

Personalization page is fully loaded with GENERAL section expanded, showing Default Personality dropdown field.

## Pass/Fail Criteria

**Pass:**
- Personalization page loads without errors
- Default Personality field is visible in GENERAL section
- Info icon is present next to field label

**Fail:**
- Page fails to load or shows errors
- Default Personality field is missing
- UI elements are misaligned or broken
