---
id: ELITEA-0972
title: "Tutorials Card Content and Links"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0972: Tutorials Card Content and Links

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Tutorials card displays the expected tutorial links and that "More..." navigates to the full tutorials listing.

**Coverage:**
- Tutorials card link list correctness
- Link navigation (no broken links)
- "More..." link presence and behavior

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected: 3 tutorial links visible in card, More... link at bottom

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads with all cards visible. |
| 2 | Locate the Tutorials card. | Card is present with correct title and subtitle. |
| 3 | Verify 3 tutorial links are listed inside the card. | 3 distinct tutorial entry links are visible. |
| 4 | Confirm a "More..." link is present at the bottom of the card. | "More..." link is visible. |
| 5 | Click each of the 3 tutorial links one by one (returning to Resources page each time). | Each link navigates to the corresponding tutorial page; no 404 or error. |
| 6 | Return to Resources page. Click More... in the Tutorials card. | Navigates to the Tutorials listing/index page; no 404 or error. |
| 7 | Confirm none of the links open a broken or empty page. | All linked destinations load content successfully. |
| 8 | Confirm all 3 tutorial entries have readable text labels (not blank or encoded characters). | All link labels are readable text. |

## Expected Final State

All link labels are readable text.

## Pass/Fail Criteria

**Pass:**
- 3 tutorial links are visible
- Each link navigates to the correct tutorial page
- "More..." navigates to the Tutorials listing

**Fail:**
- Any expected tutorial link is missing
- Any link returns a 404 or error page
- "More..." is absent or navigates incorrectly
