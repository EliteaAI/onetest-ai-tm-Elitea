---
id: ELITEA-3635
title: "Analytics — Pipeline Execution Run Counting"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, agent-pipeline, pipeline, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3635: Analytics — Pipeline Execution Run Counting

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Pipeline executions are counted accurately and separately from Agent executions.

**Coverage:**
- Pipeline runs increment AGENT & PIPELINE RUNS KPI
- Pipeline appears in Agent & Pipeline Activity table
- Multi-step pipeline tracks cumulative tokens/costs

## Preconditions

- Logged in to {{base_url}}
- At least one Pipeline is configured with multiple steps
- User has access to Settings > Analytics > Agents & Pipelines tab

## Test Data

| Field | Value |
|-------|-------|
| Pipeline Name | regression test cases generator (base) |
| Test Input | Feature description or test scenario |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Agents & Pipelines tab | Note current state for the test pipeline |
| 2 | Navigate to Pipelines. Select the test pipeline | Pipeline details page opens |
| 3 | Execute the pipeline with appropriate input | Pipeline processes through all steps |
| 4 | Navigate to Analytics > Overview tab | AGENT & PIPELINE RUNS KPI incremented |
| 5 | Navigate to Analytics > Agents & Pipelines tab | Pipeline row shows RUNS +1 |
| 6 | Verify TOTAL TOKENS for pipeline | Tokens reflect all LLM calls within pipeline |
| 7 | Verify TOTAL COST for pipeline | Cost reflects cumulative LLM usage |
| 8 | Compare pipeline's tokens with LLM model breakdown | Pipeline tokens should match or be subset of model tokens |

## Expected Final State

Pipeline execution is tracked as a single run. All tokens and costs from internal LLM calls are attributed to the pipeline.

## Pass/Fail Criteria

**Pass:**
- Pipeline run is counted in RUNS
- Total tokens = sum of all internal LLM calls
- Pipeline appears in "Most Active Agents & Pipelines" chart if applicable

**Fail:**
- Pipeline not tracked
- Tokens/costs missing or incorrect
- Internal LLM calls not aggregated to pipeline
