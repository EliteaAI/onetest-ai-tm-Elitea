---
id: ELITEA-4860
title: "Load more than 4 chat starters when a participant is added in Canvas mode"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with 10 starters exists

## Test Data

| Field | Value |
|-------|-------|
| Related regression | #4435 (Canvas mode starters) |
| Expected tiles | starters 1–3 + "+7 more" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a conversation, add the 10-starter agent as participant without reloading, and open it in Canvas mode | The agent editor shows beside the chat; the chat shows starters 1–3 + "+7 more" |
| 2 | Click "+7 more" | The popover lists all 10 and isn't clipped by the canvas container; it is inside the viewport |
| 3 | In the canvas editor, change the starters (for example remove #1) without saving | The chat tiles update live (new first 3 + "+6 more") |
| 4 | Open the popover and pick an item | Its text fills the composer |
| 5 | Leave Canvas mode without saving | The agent still has 10 stored starters |

## Expected Final State

Canvas mode loads and shows every starter without a reload. Unsaved canvas edits are not stored.

## Pass/Fail Criteria

**Pass:**
- Starters load dynamically, the popover works without clipping, and unsaved edits are reflected live but not stored

**Fail:**
- Starters need a reload to appear, show at most 4, or the popover is clipped
