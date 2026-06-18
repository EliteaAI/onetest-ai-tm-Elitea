---
id: ELITEA-0623
title: "Support Assistant panel state is shared across all application pages (global session)"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [session-state, global-state, cross-page, story:4774, r-2.0.3]
requirements: [4774, 4776]
---
# ELITEA-0623: Support Assistant panel state is shared across all application pages (global session)

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Support Assistant is not page-scoped: the same conversation is visible regardless of which application page the user is on when they open the panel. Opening the panel on the Agents page must show the same session as opening it on the Chat page.

## Preconditions

Support Assistant is enabled.
Tester is logged in as a regular user.

## Test Data

Test message sent from one page (e.g., "What is an agent?")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Chat page; open the Support Assistant and send "What is an agent?" | Message sent; response received |
| 2 | Close the Support Assistant panel | Panel closes |
| 3 | Navigate to the Pipelines page | Page loads normally |
| 4 | Open the Support Assistant from the launcher on the Pipelines page | The panel opens showing the same conversation: "What is an agent?" and its response are visible |
| 5 | Navigate to the Agents page and open the Support Assistant | Same conversation is still shown |

## Expected Final State

Same conversation is still shown

## Pass/Fail Criteria

PASS: Same conversation visible from any page; no new blank session created on navigation.
FAIL: Different or empty conversation shown on a different page; session is page-scoped.
