---
id: ELITEA-0966
title: "Environment-wide Content Consistency Across Projects"
priority: high
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0966: Environment-wide Content Consistency Across Projects

**Module:** Resources · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Resources page content is identical regardless of which project the user is viewing, confirming environment-wide consistency.

**Coverage:**
- Card link lists are identical across different projects
- Card titles and subtitles are not project-specific
- No project-level customisation applied to Resources content

## Preconditions

Logged in to ELITEA with access to at least two projects (e.g., Private workspace + a shared project)

## Test Data

Requires at least 2 different projects in the same ELITEA environment

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA and switch to Project A (e.g., Private workspace). | Project A is active. |
| 2 | Navigate to the Resources page in Project A. | Resources page loads with all 4 cards. |
| 3 | Note (or screenshot) the full list of links for all 4 cards in Project A. | Link list captured for comparison. |
| 4 | Switch to Project B (a different project in the same environment). | Project B is active. |
| 5 | Navigate to the Resources page in Project B. | Resources page loads with all 4 cards. |
| 6 | Compare the card links, card titles, and card subtitles between Project A and Project B. | All content is identical — same links, same titles, same subtitles in all 4 cards. |

## Expected Final State

All content is identical — same links, same titles, same subtitles in all 4 cards.

## Pass/Fail Criteria

**Pass:**
- All card links, titles, and subtitles are identical in Project A and Project B
- No project-specific links or content visible on the Resources page

**Fail:**
- Any card shows different links, titles, or subtitles between projects
- Project-specific content is visible on the Resources page
