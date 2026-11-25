---
id: ELITEA-0919
title: "Verify Page Scrolls to Top With 1 up to the Limit of Conversation Starters"
priority: high
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4685]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4685, EliteaAI/elitea_issues#7322]
---
# ELITEA-0919: Verify Page Scrolls to Top With 1 up to the Limit of Conversation Starters

**Module:** Pipeline Creation Ux · **Priority:** High · **Type:** Functional

**Objective:** Verify that the chat pipeline configuration panel scroll remains functional (can reach the top) after adding each conversation starter, from 1 up to the admin limit M (Admin → Features → Chat Configuration → Max Chat Starters per Version, 1–10, default 4).

**Coverage:**
- Scroll functionality at every conversation starter count from 1 to M
- Boundary condition at M conversation starters

## Preconditions

- Logged in
- Private project selected
- Chat pipeline participant configuration panel is open
- The current limit M is known (Admin → Features → Chat Configuration, or the counter "0/M starters added." in the panel)

## Test Data

| Count | Values |
|-------|--------|
| 1 | Starter 1 |
| 2 | Starter 1, Starter 2 |
| … | … |
| M | Starter 1 … Starter M |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline participant configuration panel in Chat | Panel is displayed |
| 2 | Add 1 conversation starter (Starter 1) | Starter is added; the counter reads "1/M starters added." |
| 3 | Scroll down to the bottom of the page, then scroll back to the top | Page scrolls fully to the top. Name field and page header are visible |
| 4 | Repeat steps 2–3 for Starter 2 … Starter M − 1 | Each starter is added and the page scrolls fully to the top after each one |
| 5 | Add starter M | The counter reads "M/M starters added." |
| 6 | Scroll down to the bottom, then scroll back to the top | Page scrolls fully to the top. Name field and page header remain accessible |
| 7 | Verify that no starter M + 1 can be added | The add button is disabled |

## Expected Final State

M starters are added, the page scrolls to the top, and the add button is disabled.

## Pass/Fail Criteria

**Pass:**
- After each addition (1 to M starters), scrolling to the top works without issue
- Page header and top controls (including Save/Discard) are accessible after scrolling up
- No starter beyond M can be added

**Fail:**
- After adding M starters, the page cannot be scrolled back to the top
- Top controls become inaccessible after adding any number of starters

## Notes

- Updated for #7322: the limit is no longer a fixed 4. Limit enforcement itself is covered by ELITEA-4843, ELITEA-4844 and ELITEA-4863.
