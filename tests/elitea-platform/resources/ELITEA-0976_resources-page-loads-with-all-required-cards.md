---
id: ELITEA-0976
title: "Resources Page Loads with All Required Cards"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0976: Resources Page Loads with All Required Cards

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Resources page loads successfully and displays all 4 content cards with correct titles, subtitles, and icons.

**Coverage:**
- Page title and subtitle display
- All 4 content cards present (Documentation, Release Notes, Video Library, Tutorials)
- Card icons, titles, subtitles rendered

## Preconditions

Logged in as a standard ELITEA user

## Test Data

Expected page title: Explore Resources
Expected subtitle: Guides, documentation, and release notes to support your work.
Expected cards: Documentation, Release Notes, Video Library, Tutorials

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. | Home page loads. |
| 2 | Click "Resources" in the left sidebar. | Resources page loads without error. |
| 3 | Read the main heading at the top of the page. | Heading reads "Explore Resources." |
| 4 | Read the subtitle text below the heading. | Subtitle reads "Guides, documentation, and release notes to support your work." |
| 5 | Confirm the Documentation card: document icon, title "DOCUMENTATION", subtitle "API reference, guides, and platform concepts." | Card visible with correct icon, title, and subtitle. |
| 6 | Confirm the Release Notes card: bell icon, title "RELEASE NOTES", subtitle "Product updates, improvements, and fixes." | Card visible with correct icon, title, and subtitle. |
| 7 | Confirm the Video Library card: play icon, title "VIDEO LIBRARY", subtitle "Product walkthroughs and recorded sessions." | Card visible with correct icon, title, and subtitle. |
| 8 | Confirm the Tutorials card: graduation cap icon, title "TUTORIALS", subtitle "Step-by-step guides and use cases." | Card visible with correct icon, title, and subtitle. |
| 9 | Confirm no card shows a blank body, spinner, or error message. | All 4 cards display their full content without errors. |

## Expected Final State

All 4 cards display their full content without errors.

## Pass/Fail Criteria

**Pass:**
- Page loads without errors
- Heading and subtitle match expected text exactly
- All 4 cards present with correct icons, titles, and subtitles

**Fail:**
- Page fails to load or shows an error
- Any card is missing, blank, or shows incorrect title/subtitle
- Heading or subtitle text is missing or incorrect
