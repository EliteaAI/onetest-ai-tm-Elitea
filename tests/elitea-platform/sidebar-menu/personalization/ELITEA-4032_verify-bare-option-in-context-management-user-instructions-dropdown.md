---
id: ELITEA-4032
title: "Verify Bare option in Context Management USER INSTRUCTIONS dropdown"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-4032: Verify Bare option in Context Management USER INSTRUCTIONS dropdown

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Bare option appears in Context Management modal's USER INSTRUCTIONS dropdown with correct description and persists when modal is reopened

## Preconditions

- User is logged in to `{{base_url}}`
- Context Management modal is open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Section | USER INSTRUCTIONS |
| Expected Option | Bare |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Context Management modal, scroll to "USER INSTRUCTIONS" section | USER INSTRUCTIONS section is visible |
| 2 | Locate the persona dropdown (currently showing "Generic" or another value) | Dropdown is found |
| 3 | Click on the persona dropdown | Dropdown expands showing all personality options |
| 4 | Verify dropdown shows all 7 options: Generic, QA, Nerdy, Quirky, Cynical, None, Bare | All options are visible |
| 5 | Verify "Bare" appears as the LAST option | Bare is at position 7 |
| 6 | Verify "Bare" description matches Settings page: "No Elitea identity — only your instructions plus tool-required guidance" | Description is consistent across UI |
| 7 | Select "Bare" | Selection updates immediately in dropdown |
| 8 | Close modal (click ×) | Modal closes |
| 9 | Reopen Context Management modal | Modal opens again |
| 10 | Verify USER INSTRUCTIONS dropdown shows "Bare" as selected | Selection persisted |

## Expected Final State

Context Management modal's USER INSTRUCTIONS dropdown includes "Bare" option with correct description, and selection persists.

## Pass/Fail Criteria

**Pass:**
- "Bare" option is present in Context Management dropdown
- Description matches Settings page exactly
- Selection updates and persists when modal is reopened
- No UI inconsistencies between Settings and modal

**Fail:**
- "Bare" is missing from Context Management dropdown
- Description differs from Settings page
- Selection doesn't persist
