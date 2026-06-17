---
id: ELITEA-1036
title: "Personalization Page: Create Button Shows Only `+` Instead of `+ Create`"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1036: Personalization Page: Create Button Shows Only `+` Instead of `+ Create`

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify and document that navigating to the Personalization page causes the Create button to display only `+` (no label), when it should display `+ Create` consistent with the expected design for pages without a specific entity.

**Coverage:**
- Create button label on Personalization page
- Button click and dropdown behavior on Personalization page

## Preconditions

- Logged in to ELITEA
- Sidebar in expanded state
- Access Personalization via the user profile at the bottom of the sidebar

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the user profile name at the bottom of the sidebar to open the Personalization page | Personalization page opens |
| 2 | Inspect the Create button in the sidebar | **Actual (Bug):** Button shows only `+` with no label text. **Expected:** Button should show `+ Create` |
| 3 | Click the `+` button (or the `v` arrow if visible) | Dropdown opens with all available entity types |
| 4 | Select any entity type from the dropdown | Navigation proceeds to the correct creation form |

## Expected Final State

Navigation proceeds to the correct creation form

## Pass/Fail Criteria

**Pass (after fix):**
- Personalization page shows `+ Create` label on the button
- Dropdown opens and entity selections navigate correctly

**Fail (current bug state):**
- Button shows only `+` without any label on Personalization page
- Dropdown behavior is broken or inaccessible
