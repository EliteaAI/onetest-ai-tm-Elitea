---
id: ELITEA-0249
title: "Request App Tab: Application Cards Display"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0249: Request App Tab: Application Cards Display

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that both application cards (DeepWiki and Inventory) render with all required elements.

**Coverage:**
- DeepWiki card: icon, name, description, Deepwiki chip, Configured chip
- Inventory card: icon, name, description, inventory chip, Configured chip
- Both cards show "+ Create App" and "> View Configured" buttons

## Preconditions

- Logged in as a project member
- At least one configured app of each type (DeepWiki, Inventory) exists in the project
- On the Request App tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Applications → Request App tab | DeepWiki and Inventory cards are both visible |
| 2 | Observe the DeepWiki card | Icon, name 'DeepWiki', short description, 'Deepwiki' chip, and 'Configured' chip are all present |
| 3 | Observe the Inventory card | Icon, name 'Inventory', short description, 'inventory' chip, and 'Configured' chip are all present |
| 4 | Observe the buttons on both cards | Each card shows '+ Create App' (pink/primary) and '> View Configured' (secondary) buttons |

## Expected Final State

Each card shows '+ Create App' (pink/primary) and '> View Configured' (secondary) buttons

## Pass/Fail Criteria

**Pass:**
- All elements present on both cards
- Chips and buttons render correctly

**Fail:**
- Any element missing or incorrect on either card
