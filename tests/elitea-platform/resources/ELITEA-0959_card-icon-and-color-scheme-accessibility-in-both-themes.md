---
id: ELITEA-0959
title: "Card Icon and Color Scheme Accessibility in Both Themes"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0959: Card Icon and Color Scheme Accessibility in Both Themes

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that card icon colours and background colour combinations meet basic visual contrast requirements in both Light and Dark themes — no icon or text blends invisibly into the card background.

**Coverage:**
- Icon visibility against card background in Light Mode
- Icon visibility against card background in Dark Mode
- Title and link text readability in both themes
- All 4 cards checked in each theme

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Light mode backgrounds: Documentation=sky-blue, Release Notes=peach, Video Library=lavender, Tutorials=mint
Dark mode backgrounds: Documentation=teal, Release Notes=olive-brown, Video Library=purple, Tutorials=dark-green

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page in Light Mode. | Resources page loads in Light Mode with all 4 cards visible. |
| 2 | For the Documentation card (sky-blue background): verify the card icon is clearly visible, the title "DOCUMENTATION" is readable, and all link labels are readable. | Icon and all text clearly visible against sky-blue background. |
| 3 | For the Release Notes card (peach background): verify icon, title, and links are all readable. | Icon and all text clearly visible against peach background. |
| 4 | For the Video Library card (lavender background): verify icon, title, and links are all readable. | Icon and all text clearly visible against lavender background. |
| 5 | For the Tutorials card (mint background): verify icon, title, and links are all readable. | Icon and all text clearly visible against mint background. |
| 6 | Switch to Dark Mode and repeat steps 2–5 for all 4 cards in their dark colour variants (teal, olive-brown, purple, dark green). | All card icons, titles, and link labels are clearly visible and readable in Dark Mode colour scheme. |
| 7 | Confirm no card in either theme has an icon or text that blends into the card background. | All icons and text are distinguishable from card backgrounds in both themes. |

## Expected Final State

All icons and text are distinguishable from card backgrounds in both themes.

## Pass/Fail Criteria

**Pass:**
- All 4 card icons are clearly distinguishable against card backgrounds in both themes
- Card title text is readable in both themes
- Card link text is readable in both themes
- No icon or text blends into the card background colour

**Fail:**
- Any card icon is invisible or barely visible against its background in either theme
- Any card title or link text is unreadable due to insufficient contrast in either theme
