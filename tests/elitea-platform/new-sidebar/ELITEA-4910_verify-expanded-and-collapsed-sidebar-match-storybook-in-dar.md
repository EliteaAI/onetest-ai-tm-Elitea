---
id: ELITEA-4910
title: "Verify expanded and collapsed sidebar match Storybook in dark and light themes"
priority: medium
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4910: Verify expanded and collapsed sidebar match Storybook in dark and light themes


## Preconditions

- User is logged in to `{{base_url}}`
- Storybook reference stories are available: `concepts-left-menu-explore--explore-chat` and `concepts-left-menu-explore--section-page-story` (prototype branch `feat/EL-7560/left-menu-explore`)

## Test Data

| # | Theme | Sidebar state | Page | Storybook story |
|---|-------|---------------|------|-----------------|
| 1 | Dark | Expanded | Chat | explore-chat |
| 2 | Dark | Expanded, Explore hovered | Chat | explore-chat |
| 3 | Dark | Collapsed | Section page (Skills) | section-page-story |
| 4 | Light | Expanded | Chat | explore-chat |
| 5 | Light | Expanded, Explore hovered | Chat | explore-chat |
| 6 | Light | Collapsed | Section page (Skills) | section-page-story |

Viewport: 1366 × 768

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the browser viewport to 1366 × 768 | The viewport is applied |
| 2 | Switch the app to the theme from the Test Data row | The theme is applied |
| 3 | Put the sidebar into the state and page from the row | The sidebar is in the required state |
| 4 | Open the matching Storybook story in the same theme and viewport | The reference is displayed |
| 5 | Compare the app with the story: order, spacing, row heights, icons, colours, dividers, hover/selected states | They match visually, with no unexpected differences |
| 6 | Repeat for every Test Data row | All rows match |

## Expected Final State

The sidebar matches the design in both themes and both states.

## Pass/Fail Criteria

**Pass:**
- No visible deviation from the Storybook reference in any row (except documented behaviour updates from sibling stories #7563/#7564)

**Fail:**
- Any colour, spacing, alignment or icon mismatch, or a theme that isn't applied to a sidebar element
