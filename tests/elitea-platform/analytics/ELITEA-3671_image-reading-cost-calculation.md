---
id: ELITEA-3671
title: "Analytics — Image Reading Cost Calculation"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, image-reading, costs, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6571]
---
# ELITEA-3671: Analytics — Image Reading Cost Calculation

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that an image-reading (vision) call produces a sensible, non-zero cost in Analytics > Costs, attributed to the correct model, and that mixing image-generation and image-reading calls in the same session doesn't mix up their costs.

**Coverage:**
- Image-reading call produces a non-zero cost attributed to the correct (vision) model
- Mixing image-generation and image-reading calls doesn't cross-attribute cost between models

## Preconditions

- Logged in to {{base_url}}
- Access to the image-generation tool and a (different) vision-capable chat model

## Test Data

| Field | Value |
|-------|-------|
| Image-generation prompt | "Generate an image of a city skyline" |
| Image-reading prompt | "Describe this image" (on an uploaded test image) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Costs > "Cost by Model". Note baseline for both the image-generation model and the vision chat model | Baseline recorded for both |
| 2 | Perform the image-generation call | Image is generated |
| 3 | Perform the image-reading call on the (different) vision model | Model responds |
| 4 | Navigate to Costs > "Cost by Model" | Image-generation model's cost increased by its own call only; vision model's cost increased by its own call only |
| 5 | Verify neither model's increase looks like it absorbed the other's cost | Each model's increase is independent and non-zero |

## Expected Final State

Each model's cost increase in Cost by Model matches only the call made against that specific model.

## Pass/Fail Criteria

**Pass:**
- Both models show their own non-zero cost increase
- No cross-contamination between the two models' rows

**Fail:**
- Either model's cost is $0/missing after a successful call
- Cost appears attributed to the wrong model
