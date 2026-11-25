---
id: ELITEA-4858
title: "Truncate long chat starters with a tooltip in tiles and the popover"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation exists with an agent with 10 starters as participant. Starter #2 is about 200 characters and #10 is 768 characters

## Test Data

| Element | Expected |
|---------|----------|
| Tile #2 | one line with an ellipsis; tooltip shows the full text |
| Popover item #10 (768 chars) | clamped to 2 lines with an ellipsis; tooltip shows the full text |
| Popover item #2 (≈200 chars) | at most 2 lines; if it fits in full, no tooltip is needed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Look at tile #2 | One line ending in an ellipsis |
| 2 | Hover tile #2 | The tooltip shows the full text |
| 3 | Click "+7 more" and look at items #2 and #10 | Each is at most 2 lines; #10 ends in an ellipsis |
| 4 | Hover item #10 (and #2 if it is clipped) | The tooltip shows the full text |
| 5 | Check tiles and popover items | Nothing overlaps |

## Expected Final State

Long starters never break the layout, and their full text is always available in a tooltip.

## Pass/Fail Criteria

**Pass:**
- Tiles truncate to one line and popover items clamp to 2 lines; clipped text has a full-text tooltip; nothing overlaps

**Fail:**
- Text overflows or overlaps, or clipped text has no tooltip
