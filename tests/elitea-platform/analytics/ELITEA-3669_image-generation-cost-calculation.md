---
id: ELITEA-3669
title: "Analytics — Image Generation Cost Calculation"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, image-generation, costs, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6571]
---
# ELITEA-3669: Analytics — Image Generation Cost Calculation

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that generating an image produces a sensible, non-zero cost in Analytics > Costs, attributed to the correct model.

**Coverage:**
- TOTAL COST increases after an image-generation call
- Cost by Model shows the increase attributed to the correct model
- Cost increase is proportionate to the tokens recorded for the call

## Preconditions

- Logged in to {{base_url}}
- Access to the image-generation tool in chat
- Access to Settings > Analytics > Costs tab

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Generate an image of a mountain landscape at sunset" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Costs tab | Note TOTAL COST and the image-generation model's current cost in "Cost by Model" |
| 2 | Navigate to Chats. Generate an image using the test prompt | Image is generated and returned successfully |
| 3 | Navigate back to Analytics > Costs tab | TOTAL COST has increased |
| 4 | Check "Cost by Model" for the image-generation model | The model's cost increased by a non-zero amount for this call |
| 5 | Sanity-check the cost against the model's input/output tokens for this call (Tokens tab) | Cost increase looks proportionate to the tokens consumed — not $0 or obviously too small given the tokens shown |

## Expected Final State

Image generation produces a non-zero, proportionate cost that is reflected in both TOTAL COST and the model's own row in Cost by Model.

## Pass/Fail Criteria

**Pass:**
- TOTAL COST and the model's cost both increase by a non-zero amount
- Cost looks proportionate to the tokens shown for the call

**Fail:**
- Cost shows $0 or is missing for a completed, successful image-generation call
- Cost is clearly disproportionate to the tokens shown
