---
id: ELITEA-4859
title: "Keep the chat starter grid and popover inside a 600px wide chat panel"
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
- An agent with 10 starters exists, with a conversation where it is a participant

## Test Data

| View | Width |
|------|-------|
| Participant chat | chat column about 600px (narrow browser window) |
| Agent editor → Test panel | panel at most 600px (drag the splitter) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Make the participant chat column about 600px wide | The starters grid stays 2×2 (3 tiles + "+7 more"); no horizontal scrollbar on the grid or the panel |
| 2 | Open the popover | Its whole box is inside the viewport |
| 3 | Open the agent's Test panel and drag it to at most 600px | The grid stays 2×2 with no horizontal overflow |
| 4 | Open the popover from the Test panel | Its whole box is inside the viewport |

## Expected Final State

The starters stay usable in narrow chat panels.

## Pass/Fail Criteria

**Pass:**
- The 2×2 grid is kept, with no horizontal overflow, and the popover is fully visible in both views

**Fail:**
- A horizontal scrollbar appears, tiles overflow, or the popover is cut off by the viewport
