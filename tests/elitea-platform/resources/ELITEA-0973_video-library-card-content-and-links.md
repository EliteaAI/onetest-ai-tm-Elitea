---
id: ELITEA-0973
title: "Video Library Card Content and Links"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0973: Video Library Card Content and Links

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Video Library card displays the expected video links and that "More..." navigates to the full video library.

**Coverage:**
- Video Library card link list correctness
- Link navigation (no broken links)
- "More..." link presence and behavior

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected: 4 video links visible in card, More... link at bottom

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads with all cards visible. |
| 2 | Locate the Video Library card. | Card is present with correct title and subtitle. |
| 3 | Verify 4 video links are listed inside the card. | 4 distinct video entry links are visible. |
| 4 | Confirm a "More..." link is present at the bottom of the card. | "More..." link is visible. |
| 5 | Click each of the 4 video links one by one (returning to Resources page each time). | Each link navigates to the corresponding video/playlist page; no 404 or error. |
| 6 | Return to Resources page. Click More... in the Video Library card. | Navigates to the Video Library index/listing page; no 404 or error. |

## Expected Final State

Navigates to the Video Library index/listing page; no 404 or error.

## Pass/Fail Criteria

**Pass:**
- All 4 expected video links are visible
- Each video link navigates to the correct video page
- "More..." navigates to the Video Library index

**Fail:**
- Any expected link is missing
- Any link returns a 404 or error page
- "More..." is absent or navigates incorrectly
