---
id: ELITEA-0968
title: "Theme Switch Preserves Resources Page State"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0968: Theme Switch Preserves Resources Page State

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching themes (Dark ↔ Light) while on the Resources page does not navigate away from the page and all card content remains intact after the switch.

**Coverage:**
- User remains on Resources page after theme switch
- All cards and links remain visible post-switch
- No page reload or content loss

## Preconditions

Logged in to ELITEA; on the Resources page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page and confirm all 4 cards are visible. | Resources page loads with all 4 cards visible. |
| 2 | Switch to Dark Mode using the theme toggle. | Theme changes to Dark Mode; user stays on Resources page. |
| 3 | Confirm all 4 cards are still present and their links are visible. | All 4 cards and links intact in Dark Mode. |
| 4 | Switch back to Light Mode using the theme toggle. | Theme changes to Light Mode; user stays on Resources page. |
| 5 | Confirm all 4 cards are still present and their links are visible. | All 4 cards and links intact in Light Mode. No content loss from either theme switch. |

## Expected Final State

All 4 cards and links intact in Light Mode. No content loss from either theme switch.

## Pass/Fail Criteria

**Pass:**
- User stays on Resources page after Dark→Light switch
- User stays on Resources page after Light→Dark switch
- All 4 cards and their links remain intact after both switches

**Fail:**
- User is navigated away from Resources page on theme switch
- Any card or link disappears after theme switch
- Page shows an error or requires a reload to restore content
