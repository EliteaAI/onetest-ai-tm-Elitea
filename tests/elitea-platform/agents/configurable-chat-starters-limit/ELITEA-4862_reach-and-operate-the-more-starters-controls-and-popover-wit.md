---
id: ELITEA-4862
title: "Reach and operate the more-starters controls and popover with the keyboard"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with 10 starters exists, with a conversation where it is a participant

## Test Data

| Control | Keys | Expected |
|---------|------|----------|
| "Show 6 more" (new chat) | Tab, Enter, Space | visible focus; Enter expands, Space collapses; `aria-expanded` follows |
| "+7 more" tile (participant chat) | Tab, Enter, Esc | visible focus; `aria-expanded` false → true; Esc closes |
| Popover items | Tab or arrow keys, Enter | visible focus in order; Enter fills the composer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a new chat with the agent, Tab to "Show 6 more" | It has visible focus |
| 2 | Press Enter | 10 rows, "Show less", `aria-expanded="true"` |
| 3 | Press Space | 4 rows, "Show 6 more", `aria-expanded="false"` |
| 4 | In the participant chat, Tab to "+7 more" | Visible focus; `aria-expanded="false"` |
| 5 | Press Enter | The popover opens; `aria-expanded="true"` |
| 6 | Move through the items with Tab or the arrow keys | Each item gets visible focus, in order |
| 7 | Press Enter on an item | The popover closes and the item's text fills the composer |
| 8 | Open the popover again with the keyboard and press Esc | The popover closes; `aria-expanded="false"`; focus is back on "+7 more" |

## Expected Final State

Every more-starters control can be used without a mouse, and focus is never lost after Esc.

## Pass/Fail Criteria

**Pass:**
- All controls are reachable with visible focus, work with Enter/Space, expose `aria-expanded`, and Esc returns focus to the tile

**Fail:**
- A control can't be reached or activated with the keyboard, `aria-expanded` is missing or wrong, or focus is lost after Esc
