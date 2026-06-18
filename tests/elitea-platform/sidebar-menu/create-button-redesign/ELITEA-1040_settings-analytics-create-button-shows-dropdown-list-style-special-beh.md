---
id: ELITEA-1040
title: "Settings > Analytics: Create Button Shows Dropdown-List Style (Special Behavior)"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1040: Settings > Analytics: Create Button Shows Dropdown-List Style (Special Behavior)

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Settings > Analytics section displays the Create button in the dropdown-list style (no entity label), consistent with the Figma-defined special behavior for Analytics.

**Coverage:**
- Analytics Create button visual style
- Dropdown opens with all entity types

## Preconditions

- Logged in to ELITEA with admin permissions
- Sidebar in expanded state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Analytics | Analytics page loads |
| 2 | Inspect the Create button appearance in the sidebar | Button shows no specific entity label; displays dropdown-list / general style (not `+ EntityName` split button) |
| 3 | Click the Create button | Dropdown opens listing all entity types |
| 4 | Select any entity type from the dropdown | Navigation proceeds to the correct creation form for that type |

## Expected Final State

Navigation proceeds to the correct creation form for that type

## Pass/Fail Criteria

**Pass:**
- Analytics Create button does not show an entity-specific label
- Dropdown opens and all entity types are available

**Fail:**
- Analytics shows an entity-specific label (e.g., `+ Agent`) erroneously
- Dropdown does not open or is empty
