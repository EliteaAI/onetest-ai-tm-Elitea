---
id: ELITEA-0963
title: "Right-Column Cards Not Cut Off at Intermediate Window Widths"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0963: Right-Column Cards Not Cut Off at Intermediate Window Widths

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that right-column cards (Release Notes, Tutorials) are not partially clipped or hidden behind the viewport edge at intermediate browser window widths before the layout switches to single-column.

**Coverage:**
- Right-column card full visibility at ~900px width
- No horizontal scroll required to read right-column card content
- Layout behaviour at intermediate widths (pre-reflow)

## Preconditions

Logged in to ELITEA; on the Resources page
Browser window resizable

## Test Data

Test width: ~900px
Right-column cards to check: Release Notes, Tutorials

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads with all 4 cards visible. |
| 2 | Resize the browser window to approximately 900px wide. | Window is resized to ~900px. |
| 3 | Inspect the Release Notes card (right column, top row). | Full card content (title, subtitle, links) is either fully visible or the layout has switched to single column. No partial clipping. |
| 4 | Inspect the Tutorials card (right column, bottom row). | Full card content (title, subtitle, links) is either fully visible or the layout has switched to single column. No partial clipping. |
| 5 | Confirm no horizontal scrollbar is required to read the right-column card content. | No horizontal scroll needed to view Release Notes or Tutorials card content. |

## Expected Final State

No horizontal scroll needed to view Release Notes or Tutorials card content.

## Pass/Fail Criteria

**Pass:**
- Right-column cards (Release Notes, Tutorials) are fully visible at ~900px
- No horizontal scroll required to view right-column card content
- OR the layout has already reflowed to single column, which is also acceptable

**Fail:**
- Right-column cards are partially cut off and require horizontal scrolling to view
- Card title, subtitle, or links are obscured by the viewport edge
