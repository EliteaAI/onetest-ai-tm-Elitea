---
id: ELITEA-4850
title: "Open, scroll and close the All chat starters popover with 10 items"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation exists with an agent with 10 chat starters as participant; the composer is empty and "+7 more" is shown

## Test Data

| Field | Value |
|-------|-------|
| Popover title | "All chat starters" |
| Visible rows | at most 6, then scrolls |
| Item click | fills the composer, like a tile (since EL-5074); nothing is sent |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click "+7 more" | The popover opens above the tile grid and lists all 10 in configured order |
| 2 | Check the popover height | At most 6 rows are visible; item #7 and later need scrolling |
| 3 | Scroll to the bottom | Item #10 is reachable |
| 4 | Press Esc | The popover closes; no message is sent; the composer is unchanged |
| 5 | Open it again and click outside it | It closes; no message is sent; the composer is unchanged |
| 6 | Open it again and click item #9 | The popover closes and item #9's text is put into the composer, as a tile click does |

## Expected Final State

The popover closes without sending anything. Item #9's text is in the composer.

## Pass/Fail Criteria

**Pass:**
- All 10 items in order, at most 6 visible with scrolling; Esc and an outside click close it without sending; an item acts like a tile

**Fail:**
- Items are missing or clipped, the popover can't scroll, or closing it sends a message
