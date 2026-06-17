---
id: ELITEA-0974
title: "Release Notes Card Content and Links"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0974: Release Notes Card Content and Links

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Release Notes card displays the expected links and that "More..." navigates to the full release notes listing.

**Coverage:**
- Release Notes card link list (including latest release label)
- Navigation correctness for each link
- "More..." link presence and behavior

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected: Latest label on current release, historical versions (R 2.0.1, R 2.0.0, R 1.x), More... link

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads with all cards visible. |
| 2 | Locate the Release Notes card. | Card is present with correct title and subtitle. |
| 3 | Confirm the most recent release entry shows a "Latest" badge/label. | "Latest" badge is visible next to the current version entry. |
| 4 | Verify at least 3 additional historical release links (e.g., R 2.0.1, R 2.0.0, R 1.x) are listed below the latest. | Historical release links are visible. |
| 5 | Confirm a "More..." link is present at the bottom of the card. | "More..." link is visible. |
| 6 | Click the latest release entry. | Navigates to the correct latest release notes page; no 404 or error. |
| 7 | Return to Resources page. Click one historical release entry. | Navigates to the corresponding historical release notes page; no error. |
| 8 | Return to Resources page. Click More... in the Release Notes card. | Navigates to the full Release Notes listing/index page; no 404 or error. |

## Expected Final State

Navigates to the full Release Notes listing/index page; no 404 or error.

## Pass/Fail Criteria

**Pass:**
- "Latest" label visible on the most recent release entry
- All expected historical release links present
- "More..." navigates to the release notes listing

**Fail:**
- "Latest" label absent
- Any release link missing or broken
- "More..." absent or navigates to incorrect page
