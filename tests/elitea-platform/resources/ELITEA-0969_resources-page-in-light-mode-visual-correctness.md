---
id: ELITEA-0969
title: "Resources Page in Light Mode — Visual Correctness"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0969: Resources Page in Light Mode — Visual Correctness

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify the Resources page renders correctly in Light Mode, with correct pastel card background colours, icon legibility, and readable text.

**Coverage:**
- Light mode card colour scheme (sky blue, peach, lavender, mint)
- Icon and text legibility against pastel card backgrounds
- "Light theme" tooltip confirmation on theme switch
- No layout breakage or invisible elements in light mode

## Preconditions

Logged in to ELITEA; on the Resources page; starting in Dark Mode

## Test Data

Expected light mode card colours: Documentation=sky-blue, Release Notes=peach, Video Library=lavender, Tutorials=mint

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Start in Dark Mode on the Resources page. | Resources page visible in dark mode. |
| 2 | Hover over the theme toggle icon (top-right area) to see its tooltip label. | Tooltip reads "Light theme". |
| 3 | Click the theme toggle to switch to Light Mode. | ELITEA switches to Light Mode; page background lightens. |
| 4 | Verify the Documentation card has a sky-blue/light-blue background. | Card background is sky-blue; icon and title clearly visible. |
| 5 | Verify the Release Notes card has a peach background. | Card background is peach; icon and title clearly visible. |
| 6 | Verify the Video Library card has a lavender background. | Card background is lavender; icon and title clearly visible. |
| 7 | Verify the Tutorials card has a mint/light-green background. | Card background is mint-green; icon and title clearly visible. |

## Expected Final State

Card background is mint-green; icon and title clearly visible.

## Pass/Fail Criteria

**Pass:**
- ELITEA switches to Light Mode; "Light theme" tooltip confirmed
- All 4 cards visible with distinct pastel colour backgrounds
- Icons and text legible against pastel backgrounds

**Fail:**
- Page fails to switch to Light Mode
- Any card appears washed-out or invisible
- Light mode card colours do not match expected pastel palette
- "Light theme" tooltip absent when hovering the theme toggle
