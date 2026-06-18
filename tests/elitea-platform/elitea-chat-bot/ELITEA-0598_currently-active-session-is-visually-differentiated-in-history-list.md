---
id: ELITEA-0598
title: "Currently active session is visually differentiated in history list"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0598: Currently active session is visually differentiated in history list

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the currently active support session is visually distinguished from past sessions in the history list.

**Coverage:**
- Visual differentiation (highlight, label, icon, etc.) applied to the active session
- Differentiation persists after scrolling or reopening history

## Preconditions

- Logged in on {{base_url}}
- An active/current support session exists alongside at least 2 past sessions

## Test Data

- Active session: current session started in this test run
- Past sessions: 2 or more previously completed sessions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant widget | Widget shows current active session |
| 2 | Click 'Chat history' (🕐) icon | History panel opens |
| 3 | Identify the current/active session in the list | The active session has a distinct visual treatment (highlight, bold, icon, 'active' label, or similar) compared to past sessions |
| 4 | Close history panel and reopen it | The same session retains its active visual state |

## Expected Final State

The same session retains its active visual state

## Pass/Fail Criteria

**Pass:**
- Active session is visually distinct from past sessions
- Differentiation is consistent on reopen

**Fail:**
- All sessions appear identical with no differentiation
- Wrong session is marked as active
