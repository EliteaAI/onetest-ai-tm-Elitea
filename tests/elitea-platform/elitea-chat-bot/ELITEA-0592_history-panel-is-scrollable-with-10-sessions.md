---
id: ELITEA-0592
title: "History panel is scrollable with 10+ sessions"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0592: History panel is scrollable with 10+ sessions

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the history panel handles a large number of sessions gracefully with scrolling or pagination.

**Coverage:**
- Scrollable history list
- No layout overflow or UI breakage with many sessions

## Preconditions

- Logged in on {{base_url}}
- User account has 10+ completed support sessions

## Test Data

- User with 10–20 past sessions
- History panel viewport height: default compact widget

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant and click 'Chat history' (🕐) | History panel opens |
| 2 | Observe the list | Sessions are displayed in a scrollable container; no content overflows outside the panel boundary |
| 3 | Scroll down within the history panel | Additional sessions become visible as the user scrolls; no sessions are cut off |
| 4 | Scroll back to top | Most recent session is at the top as before |

## Expected Final State

Most recent session is at the top as before

## Pass/Fail Criteria

**Pass:**
- All sessions accessible via scroll
- No overflow or visual breakage

**Fail:**
- Panel breaks layout with many sessions
- Sessions beyond the visible count are inaccessible
