---
id: ELITEA-4238
title: Run button visible on published Catalog skill card
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-run, catalog, chat, participant, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4238: Run button visible on published Catalog skill card

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Run button (play icon) is visible on published Catalog skill cards and can be clicked to create a chat.

**Coverage:**
- Run button appears on Catalog skill cards
- Button is enabled and clickable
- Entry point for running Catalog skills

## Preconditions

- User is logged in to {{base_url}}
- At least one skill is published to Catalog (e.g., "animal-joke")
- User has permission to access Catalog

## Test Data

- Catalog skill: "animal-joke" (or any published skill)
- Expected: Run button (play icon) visible and clickable

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Catalog page | Catalog page opens successfully |
| 2 | Click on "Skills" tab | Skills tab displays published skills in card view |
| 3 | Locate a published skill card (e.g., "animal-joke") | Skill card displays with skill icon, name, description |
| 4 | Observe the Run button (play icon) on the skill card | Run button (play icon) is visible and appears enabled |
| 5 | Verify button styling and placement | Button appears alongside other action buttons (like/heart icon) |
| 6 | Hover over the Run button | Button shows hover state (visual feedback) |

## Expected Final State

Run button (play icon) is visible and clickable on all published Catalog skill cards.

## Pass/Fail Criteria

**Pass:** Run button is visible, enabled, and shows proper hover state on Catalog skill cards.

**Fail:** Run button is missing, disabled, or incorrectly styled.
