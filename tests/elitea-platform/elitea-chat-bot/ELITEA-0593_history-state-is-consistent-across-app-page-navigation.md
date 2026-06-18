---
id: ELITEA-0593
title: "History state is consistent across app page navigation"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0593: History state is consistent across app page navigation

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the Support Assistant widget retains the same history and active session state as the user navigates between ELITEA pages.

**Coverage:**
- Same history list shown on all pages
- Active session does not reset on navigation

## Preconditions

- Logged in on {{base_url}}
- A specific session is loaded in the widget (known session)

## Test Data

- Pages to navigate to: /app/chat, /app/agents, /app/toolkits
- Active session title: "Testing navigation persistence"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant; restore session 'Testing navigation persistence' from history | Session loads in widget |
| 2 | Navigate to Agents page (/app/agents) | Page loads; widget remains visible |
| 3 | Open history panel | Same session list shown; 'Testing navigation persistence' still marked as active |
| 4 | Navigate to Toolkits page (/app/toolkits) | Page loads |
| 5 | Open history panel again | Same state — session list unchanged, same active session |

## Expected Final State

Same state — session list unchanged, same active session

## Pass/Fail Criteria

**Pass:**
- History list identical across all pages
- Active session does not change on navigation

**Fail:**
- History resets or loads differently on page change
- Active session reverts to a different session
