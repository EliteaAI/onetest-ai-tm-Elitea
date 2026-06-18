---
id: ELITEA-0967
title: "Link Hover Highlight Behavior in Both Themes"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0967: Link Hover Highlight Behavior in Both Themes

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify that links inside all 4 cards display a hover highlight state when the mouse cursor is over them, and revert to the default state on mouse-out, in both Dark and Light themes.

**Coverage:**
- Hover highlight visible on links in all 4 cards
- Hover state present in Dark Mode
- Hover state present in Light Mode
- Hover state reverts on mouse-out

## Preconditions

Logged in to ELITEA; on the Resources page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Resources page in Dark Mode. | Resources page visible in Dark Mode. |
| 2 | Hover the mouse over one link in the Documentation card. | A hover highlight (background row highlight or underline) appears on the hovered link. |
| 3 | Move the cursor away from the link. | The hover highlight disappears and the link returns to its default state. |
| 4 | Repeat hover check for one link each in Release Notes, Video Library, and Tutorials cards in Dark Mode. | Each hovered link shows the highlight; each reverts correctly on mouse-out. |
| 5 | Switch to Light Mode. | Theme switches to Light Mode; Resources page remains visible. |
| 6 | Hover the mouse over one link in the Documentation card in Light Mode. | A hover highlight appears on the hovered link. |
| 7 | Repeat hover check for one link each in Release Notes, Video Library, and Tutorials cards in Light Mode. | Each hovered link shows the highlight; each reverts correctly on mouse-out in Light Mode. |

## Expected Final State

Each hovered link shows the highlight; each reverts correctly on mouse-out in Light Mode.

## Pass/Fail Criteria

**Pass:**
- Hovering over any card link shows a visible highlight (background/underline/colour change)
- Highlight visible in both Dark and Light modes
- Highlight reverts to default state on mouse-out in both themes

**Fail:**
- No hover highlight appears on links in any card
- Hover highlight only visible in one theme
- Highlight persists after cursor moves away (sticky highlight)
