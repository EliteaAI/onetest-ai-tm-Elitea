---
id: ELITEA-0970
title: "Resources Page in Dark Mode — Visual Correctness"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0970: Resources Page in Dark Mode — Visual Correctness

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify the Resources page renders correctly in Dark Mode, with correct card background colours, icon legibility, and readable text.

**Coverage:**
- Dark mode card colour scheme (teal, olive-brown, purple, dark green)
- Icon and text legibility against dark card backgrounds
- No layout breakage or invisible elements in dark mode

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected dark mode card colours: Documentation=teal, Release Notes=olive-brown, Video Library=purple, Tutorials=dark-green

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads. |
| 2 | Switch ELITEA to Dark Mode using the theme toggle (top-right area). | ELITEA switches to Dark Mode; sidebar background darkens. |
| 3 | Verify the Documentation card has a teal/dark-teal background. | Card background is teal-coloured; icon and title are clearly visible. |
| 4 | Verify the Release Notes card has an olive-brown background. | Card background is olive-brown; icon and title are clearly visible. |
| 5 | Verify the Video Library card has a purple background. | Card background is purple; icon and title are clearly visible. |
| 6 | Verify the Tutorials card has a dark-green background. | Card background is dark-green; icon and title are clearly visible. |
| 7 | Check all link text within cards for readability (not hidden or washed out). | All link labels are legible with sufficient contrast against the card background. |

## Expected Final State

All link labels are legible with sufficient contrast against the card background.

## Pass/Fail Criteria

**Pass:**
- ELITEA switches to Dark Mode without error
- All 4 cards visible with distinct dark colour backgrounds
- Card icons clearly visible against card backgrounds
- All text labels, link names, subtitles legible

**Fail:**
- Page fails to switch to Dark Mode
- Any card appears black-on-black (invisible text)
- Any icon is invisible or blends into background
- Dark mode colours do not match expected dark palette
