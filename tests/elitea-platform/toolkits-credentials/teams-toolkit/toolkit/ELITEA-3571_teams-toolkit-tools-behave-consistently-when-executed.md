---
id: ELITEA-3571
title: "Teams Toolkit Tools Behave Consistently When Executed From Agents and Pipelines"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3571: Teams Toolkit Tools Behave Consistently When Executed From Agents and Pipelines

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that invoking Teams tools from within an Agent and from within a Pipeline produces the same structured results as a direct call, and that an expired/missing token mid-execution surfaces the re-authorization flow without crashing the run.

## Preconditions

- A Teams toolkit instance linked to an authorized credential
- An Agent and a Pipeline both configurable to use the Teams toolkit

## Test Data

- N/A (see Steps)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure an Agent with the Teams toolkit; have it call at least one read tool (e.g. `list_teams`) and one write tool (e.g. `send_chat_message`) | Results match direct-call behavior in structure and content |
| 2 | Configure a Pipeline step using the Teams toolkit and repeat the same calls | Results match direct-call behavior in structure and content |
| 3 | Invalidate/expire the underlying token and re-run the Agent, then the Pipeline | Each run surfaces a re-authorization step rather than crashing or hanging |

## Expected Final State

Agent and Pipeline executions of Teams tools are behaviorally identical to direct calls, including consistent handling of an invalidated token.

## Pass/Fail Criteria

**Pass:**
- Agent and Pipeline results match direct-call results; token invalidation surfaces re-authorization cleanly in both

**Fail:**
- Agent or Pipeline results diverge from direct-call behavior, or an invalidated token crashes/hangs either run
