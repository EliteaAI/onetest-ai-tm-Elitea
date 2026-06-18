---
id: ELITEA-0254
title: "Configured Tab: Grid View Layout"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0254: Configured Tab: Grid View Layout

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Configured tab loads in grid view by default and shows all project members' apps correctly.

**Coverage:**
- Tab accessible and switches correctly
- Grid view is default (4-column)
- Each card shows icon, name, author avatar, app-type chip
- Apps from all project members are listed

## Preconditions

- Logged in as a project member
- Multiple configured apps from at least 2 different users exist in the project

## Test Data

At least 2 apps created by different project members

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the 'Configured' tab | Configured tab opens in 4-column grid view by default |
| 2 | Observe multiple app cards in the grid | Each card shows: placeholder icon, app name, author avatar, app-type chip (e.g., Deepwiki, inventory) |
| 3 | Verify apps from other project members are visible | Apps from other users are listed — not only the current user's apps |

## Expected Final State

Apps from other users are listed — not only the current user's apps

## Pass/Fail Criteria

**Pass:**
- Grid view shown by default
- All card elements present
- Multi-user apps visible

**Fail:**
- List view shown by default, card elements missing, or only current user's apps visible
