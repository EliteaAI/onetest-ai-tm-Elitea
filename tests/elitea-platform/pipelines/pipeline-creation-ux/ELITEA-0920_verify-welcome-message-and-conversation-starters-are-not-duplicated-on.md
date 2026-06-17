---
id: ELITEA-0920
title: "Verify Welcome Message and Conversation Starters Are Not Duplicated on Scroll"
priority: high
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4684]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4684]
---
# ELITEA-0920: Verify Welcome Message and Conversation Starters Are Not Duplicated on Scroll

**Module:** Pipeline Creation Ux · **Priority:** High · **Type:** Functional

**Objective:** Verify that Welcome Message and Conversation Starters fields appear exactly once in the chat pipeline configuration panel and are not duplicated when scrolling.

**Coverage:**
- UI element deduplication on scroll in chat pipeline config panel

## Preconditions

- Logged in
- Private project selected
- Chat pipeline participant configuration panel is open

## Test Data

- Welcome Message: Welcome to test pipeline
- Conversation Starters: How can you help?, What can you do?

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline participant configuration panel in Chat | Configuration panel is displayed |
| 2 | Enter a Welcome Message (Welcome to test pipeline) | Welcome Message field is populated once |
| 3 | Add 2 conversation starters: How can you help? and What can you do? | Both conversation starters are added. Each appears once in the list |
| 4 | Scroll down to the bottom of the page | Page scrolls down |
| 5 | Scroll back upward slowly through the entire page | All fields observed during scrolling |
| 6 | Observe the Welcome Message field during the full scroll cycle | Welcome Message field appears exactly once |
| 7 | Observe the Conversation Starters list during the full scroll cycle | Each conversation starter text appears exactly once in the list |

## Expected Final State

Each conversation starter text appears exactly once in the list

## Pass/Fail Criteria

**Pass:**
- Welcome Message field appears exactly once throughout the scroll
- Each conversation starter entry appears exactly once

**Fail:**
- Welcome Message field is rendered twice during any point of the scroll
- Any conversation starter entry is duplicated in the visible UI
