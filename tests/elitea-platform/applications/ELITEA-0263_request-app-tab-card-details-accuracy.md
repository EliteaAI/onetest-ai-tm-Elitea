---
id: ELITEA-0263
title: "Request App Tab: Card Details Accuracy"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0263: Request App Tab: Card Details Accuracy

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that card descriptions, status chips, and layout are accurate and consistent on the Request App tab.

**Coverage:**
- Exact description texts for DeepWiki and Inventory
- Configured chip accuracy based on actual configured apps
- Consistent card height and button alignment

## Preconditions

- Logged in as a project member
- On the Request App tab

## Test Data

DeepWiki expected description: 'Generate searchable wiki pages from repository code and keep architecture context close to delivery work.'
Inventory expected description: 'Explore services, ownership, dependencies, and technical inventory across project repositories.'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Read the DeepWiki card description text | Text matches: 'Generate searchable wiki pages from repository code and keep architecture context close to delivery work.' |
| 2 | Read the Inventory card description text | Text matches: 'Explore services, ownership, dependencies, and technical inventory across project repositories.' |
| 3 | Observe the Configured chip on each card | Chip is shown only when at least one app of that type exists in the project |
| 4 | Compare both cards visually | Both cards have consistent height and vertical button alignment |

## Expected Final State

Both cards have consistent height and vertical button alignment

## Pass/Fail Criteria

**Pass:**
- All description texts match expected values exactly
- Configured chip is accurate
- Cards have consistent visual layout

**Fail:**
- Text mismatch, chip incorrectly shown/hidden, or cards have inconsistent layout
