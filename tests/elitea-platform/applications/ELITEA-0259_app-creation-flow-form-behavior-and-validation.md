---
id: ELITEA-0259
title: "App Creation Flow: Form Behavior and Validation"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0259: App Creation Flow: Form Behavior and Validation

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify the app creation form validates mandatory fields correctly and that new apps appear immediately in the Configured tab.

**Coverage:**
- Form pre-fills correct app type from card and modal entry points
- Mandatory field validation on empty submit
- Newly created app appears in Configured tab immediately

## Preconditions

- Logged in as a project member with permission to create apps
- A valid toolkit is configured for DeepWiki
- On the Request App tab

## Test Data

Valid app name for DeepWiki; valid required configuration fields

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click '+ Create App' on the DeepWiki card | Form opens pre-set to DeepWiki type |
| 2 | Click '+ Create App' inside the DeepWiki modal | Form opens pre-set to DeepWiki type |
| 3 | On the creation form, clear all mandatory fields and click Save | Field-level validation errors appear; form is not submitted |
| 4 | Fill in all mandatory fields with valid data and click Save | App is created successfully |
| 5 | Navigate to the Configured tab | Newly created app appears immediately without requiring a page refresh |

## Expected Final State

Newly created app appears immediately without requiring a page refresh

## Pass/Fail Criteria

**Pass:**
- Type pre-filled correctly from both entry points
- Validation shown on empty mandatory fields
- New app visible in Configured tab immediately after creation

**Fail:**
- Wrong type pre-filled, no validation on empty fields, or app not appearing after creation
