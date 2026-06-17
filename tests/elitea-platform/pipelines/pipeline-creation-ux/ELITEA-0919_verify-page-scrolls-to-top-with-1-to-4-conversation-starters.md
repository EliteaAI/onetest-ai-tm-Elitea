---
id: ELITEA-0919
title: "Verify Page Scrolls to Top With 1 to 4 Conversation Starters"
priority: high
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4685]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4685]
---
# ELITEA-0919: Verify Page Scrolls to Top With 1 to 4 Conversation Starters

**Module:** Pipeline Creation Ux · **Priority:** High · **Type:** Functional

**Objective:** Verify that the chat pipeline configuration panel scroll remains functional (can reach the top) after adding 1, 2, 3, and 4 conversation starters — which is the maximum allowed.

**Coverage:**
- Scroll functionality at all conversation starter counts (1–4, max allowed)
- Boundary condition at maximum 4 conversation starters

## Preconditions

- Logged in
- Private project selected
- Chat pipeline participant configuration panel is open

## Test Data

Count | Values
1 | Starter 1
2 | Starter 1, Starter 2
3 | Starter 1, Starter 2, Starter 3
4 | Starter 1, Starter 2, Starter 3, Starter 4

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline participant configuration panel in Chat | Panel is displayed |
| 2 | Add 1 conversation starter (Starter 1) | Starter is added |
| 3 | Scroll down to the bottom of the page, then scroll back to the top | Page scrolls fully to the top. Name field and page header are visible |
| 4 | Add a second conversation starter (Starter 2) | Second starter is added |
| 5 | Scroll down, then scroll back to the top | Page scrolls fully to the top |
| 6 | Add a third conversation starter (Starter 3) | Third starter is added |
| 7 | Scroll down, then scroll back to the top | Page scrolls fully to the top |
| 8 | Add a fourth conversation starter (Starter 4) | Fourth starter is added. This is the maximum (4) |
| 9 | Scroll down to the bottom, then scroll back to the top | Page scrolls fully to the top. Name field and page header remain accessible |
| 10 | Verify that no fifth conversation starter can be added | Adding a 5th starter is either blocked or the add button is disabled |

## Expected Final State

Adding a 5th starter is either blocked or the add button is disabled

## Pass/Fail Criteria

**Pass:**
- After each addition (1–4 starters), scrolling to the top works without issue
- Page header and top controls (including Save/Discard) are accessible after scrolling up
- No 5th conversation starter can be added (max is 4)

**Fail:**
- After adding 4 starters, the page cannot be scrolled back to the top
- Top controls become inaccessible after adding any number of starters
