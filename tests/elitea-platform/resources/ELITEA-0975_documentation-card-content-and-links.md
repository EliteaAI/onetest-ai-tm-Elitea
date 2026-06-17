---
id: ELITEA-0975
title: "Documentation Card Content and Links"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0975: Documentation Card Content and Links

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Documentation card displays the correct links and that each link (including "More...") navigates to the correct destination.

**Coverage:**
- Documentation card link list correctness
- Link navigation behavior (no broken links)
- "More..." action present and functional

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected links: Getting Started, How-To Guides, Integrations, Migration & Update, More...

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads with all cards visible. |
| 2 | Locate the Documentation card. | Card is present with correct title and subtitle. |
| 3 | Verify links visible: Getting Started, How-To Guides, Integrations, Migration & Update. | All 4 links are present and visible inside the card. |
| 4 | Confirm a "More..." link is present at the bottom of the card. | "More..." link is visible. |
| 5 | Click Getting Started. | Navigates to the Getting Started documentation page; no 404 or error. |
| 6 | Return to Resources page. Click How-To Guides. | Navigates to the How-To Guides page; no 404 or error. |
| 7 | Return to Resources page. Click Integrations. | Navigates to the Integrations documentation page; no 404 or error. |
| 8 | Return to Resources page. Click Migration & Update. | Navigates to the Migration & Update page; no 404 or error. |
| 9 | Return to Resources page. Click More... in the Documentation card. | Navigates to the main Documentation index/listing page; no 404 or error. |

## Expected Final State

Navigates to the main Documentation index/listing page; no 404 or error.

## Pass/Fail Criteria

**Pass:**
- All 4 expected links are present
- "More..." link is present
- Every link navigates to the correct, non-error destination

**Fail:**
- Any expected link is missing
- Any link returns a 404 or error page
- "More..." is missing or navigates incorrectly
