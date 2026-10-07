---
id: ELITEA-3701
title: "Verify Nested Agent + Skill Execution Reconciles With LiteLLM on Cost and Tokens"
priority: critical
type: integration
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6705]
---

# ELITEA-3701: Verify Nested Agent + Skill Execution Reconciles With LiteLLM on Cost and Tokens

**Module:** Analytics · **Priority:** Critical · **Type:** Integration

**Objective:** Verify a multi-level agent/skill execution reconciles with LiteLLM on both cost and tokens — the exact scenario reported in issue #6705, where cost and tokens diverged in opposite directions.

**Coverage:**
- Nested agent → sub-agent → skills chain total cost/tokens reconcile with LiteLLM
- No opposite-direction divergence between cost and token deltas

## Preconditions

- Admin/owner access to a DEV project with Analytics and matching LiteLLM logs
- Ability to attach a sub-agent and skills to a parent agent

## Test Data

| Field | Value |
|-------|-------|
| Parent agent "agent" | model: platform-managed shared model; attached skill "formatter-skill" ("Format everything for uppercase") |
| Sub-agent "animals teller" | attached to "agent"; instruction: "generate 2 sentences about animal user requested" |
| Skill "cat's teller" | attached to "animals teller"; underscore-delimited output |
| Skill "dog's teller" | attached to "animals teller"; uppercase output |
| Input | "tell me about dogs" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Build the structure described in Test Data | Structure saved successfully |
| 2 | Execute "agent" once with input "tell me about dogs" | Execution completes |
| 3 | Note the execution's time window / request ids | Captured |
| 4 | Sum LiteLLM cost/tokens across every call in the chain (parent, sub-agent, each skill) | Total LiteLLM figures recorded |
| 5 | Open Settings > Analytics (Overview/Costs/Tokens and the Agents & Pipelines tab's run detail) for the same window | Analytics totals recorded |
| 6 | Compare Analytics totals vs LiteLLM sums | Totals reconcile within expected rounding tolerance |
| 7 | Check the direction of any discrepancy | Cost and token deltas (if any) are consistent in direction — NOT one under-reported while the other is over-reported |

## Expected Final State

Analytics' cost and token totals for the nested agent+skill run match the LiteLLM-derived totals for the same execution within rounding tolerance, with no opposite-direction divergence.

## Pass/Fail Criteria

**Pass:**
- Analytics total cost and total tokens are within expected rounding tolerance of the LiteLLM sums

**Fail:**
- Analytics cost and LiteLLM cost diverge beyond rounding tolerance
- Analytics tokens and LiteLLM tokens diverge beyond rounding tolerance
- Cost and tokens diverge in opposite directions (one over-reported, one under-reported)
