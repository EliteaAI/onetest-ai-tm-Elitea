---
id: ELITEA-3493
title: "Guide Tab Documentation Display"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3493: Guide Tab Documentation Display

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Guide tab displays complete documentation for all Analytics metrics.

## Preconditions

- Logged into {{base_url}}
- Navigate to Settings → Analytics → Guide

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Guide" tab. | Guide documentation loads. |
| 2 | Verify "Overview Tab" section present. | Section header visible with metric explanations. |
| 3 | Verify TEAM metric documentation. | Shows description, Calculation formula, Data source. |
| 4 | Verify AI ACTIVE metric documentation. | Explains what counts as AI active user. |
| 5 | Verify LLM CALLS documentation. | Shows Calculation: event_type = "llm", Data source listed. |
| 6 | Verify TOOL RUNS documentation. | Shows Calculation: event_type = "tool". |
| 7 | Verify CHAT MSG documentation. | Explains action = "SIO chat_predict". |
| 8 | Verify AGENT & PIPELINE RUNS documentation. | Explains what counts as a run. |
| 9 | Scroll through entire guide. | All metrics have descriptions, calculations, and data sources. |
| 10 | Verify text is readable (not truncated). | Full documentation visible without overflow. |

## Pass/Fail Criteria

**Pass:** All metrics documented with description, calculation formula, and data source.
**Fail:** Missing metrics, incomplete explanations, or text overflow issues.
