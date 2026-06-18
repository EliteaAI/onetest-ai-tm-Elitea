---
id: ELITEA-1300
title: "Speaking Mode Button vs. Send Button — Input Field State [Chat, Agent, Pipeline]"
priority: critical
type: functional
module: speaking-mode
status: draft
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1300: Speaking Mode Button vs. Send Button — Input Field State [Chat, Agent, Pipeline]

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Speaking Mode button shows instead of Send when the input is empty, and switches to Send when typing — on Chat (existing conversation), Agent, and Pipeline pages.

**Coverage:** Button state changes between Speaking Mode and Send based on input content; consistent across all 3 pages.

## Preconditions

- Logged in at {{base_url}} Chrome or Edge; mic permission granted
- An existing Chat conversation with at least 1 message; 1 Agent and 1 Pipeline exist

## Test Data

Any short text string (e.g., "Hello")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing Chat conversation (≥1 message). Clear the input field. | Speaking Mode button visible in toolbar |
| 2 | Type "Hello" into the input field. | Button switches to Send |
| 3 | Delete the text so the input is empty again. | Speaking Mode button reappears |
| 4 | Open an Agent execution panel. Type text, then clear. | Same toggle behavior — Speaking Mode on empty, Send on typing |
| 5 | Open a Pipeline execution panel. Type text, then clear. | Same toggle behavior on Pipeline page |

## Expected Final State

Same toggle behavior on Pipeline page

## Pass/Fail Criteria

**Pass:**
- Speaking Mode button correctly visible on all 3 pages when input is empty
- Button correctly switches between Speaking Mode and Send on all 3 pages

**Fail:**
- Speaking Mode button missing on any page
- Button does not toggle correctly on any page
