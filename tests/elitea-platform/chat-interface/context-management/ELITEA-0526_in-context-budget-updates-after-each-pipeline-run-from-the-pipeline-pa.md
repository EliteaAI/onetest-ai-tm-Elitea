---
id: ELITEA-0526
title: "In-Context Budget Updates After Each Pipeline Run From the Pipeline Page"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:context-management, feat:pipelines, issue:4325, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4325]
---
# ELITEA-0526: In-Context Budget Updates After Each Pipeline Run From the Pipeline Page

**Module:** Context Management · **Priority:** High · **Type:** Functional

## Preconditions

- Logged in to {{base_url}}
- Pipeline page is open for any existing pipeline
- In-context budget widget is visible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline page for any pipeline. | Pipeline editor/runner is displayed. In-context budget shows initial values (0 messages, 0 tokens). |
| 2 | Execute the pipeline (Run 1). After it completes, note the in-context budget: message count M1 and token count T1. | Pipeline completes. Budget shows M1 > 0 and T1 > 0. |
| 3 | Execute the pipeline again without navigating away (Run 2). After it completes, note the budget: message count M2 and token count T2. | Budget updates: M2 > M1 and T2 > T1. |
| 4 | Execute the pipeline a third time (Run 3). After it completes, note the budget: message count M3 and token count T3. | Budget updates again: M3 > M2 and T3 > T2. |

## Expected Final State

Budget updates again: M3 > M2 and T3 > T2.

## Pass/Fail Criteria

**Pass:** Message count and token count in the in-context budget increase after each consecutive pipeline run (M1 < M2 < M3, T1 < T2 < T3).
**Fail:** After Run 1, subsequent runs show the same M1/T1 values — the budget is frozen at first-run results.
