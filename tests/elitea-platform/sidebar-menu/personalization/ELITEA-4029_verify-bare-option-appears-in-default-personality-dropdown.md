---
id: ELITEA-4029
title: "Verify Bare option appears in Default Personality dropdown"
priority: critical
type: functional
module: personalization
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-4029: Verify Bare option appears in Default Personality dropdown

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Bare personality option appears in the Default Personality dropdown with correct description and position

## Preconditions

- User is logged in to `{{base_url}}`
- Personalization page is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/personalization` |
| Expected Option | Bare |
| Expected Description | No Elitea identity — only your instructions plus tool-required guidance |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Personalization | Personalization page loads |
| 2 | Click on "Default Personality" dropdown (currently showing "Generic") | Dropdown expands showing all personality options |
| 3 | Verify dropdown shows all 7 options in order: Generic, QA, Nerdy, Quirky, Cynical, None, Bare | All 7 options are visible in correct order |
| 4 | Verify "Bare" appears as the LAST option (position 7) | Bare is at the bottom of the list |
| 5 | Verify "Bare" option shows description: "No Elitea identity — only your instructions plus tool-required guidance" | Description text is displayed correctly below option name |
| 6 | Verify each option displays name in bold + description in lighter text | Consistent formatting across all options |

## Expected Final State

Dropdown displays all 7 personality options with "Bare" as the last option, showing correct description text.

## Pass/Fail Criteria

**Pass:**
- All 7 personality options are visible
- "Bare" appears in position 7 (last)
- Description matches exactly: "No Elitea identity — only your instructions plus tool-required guidance"
- Formatting is consistent with other options

**Fail:**
- "Bare" option is missing
- "Bare" appears in wrong position
- Description text is incorrect or missing
- Dropdown has layout issues
