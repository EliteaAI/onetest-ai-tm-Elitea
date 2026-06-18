---
id: ELITEA-0135
title: "Swarm Mode - Child Agent Invocation Consistency"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0135: Swarm Mode - Child Agent Invocation Consistency

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that all configured child agents in swarm mode are invoked consistently when needed.

## Preconditions

User logged into Elitea stage.elitea.ai\nAt least 2 child agents exist with distinct tools/prompts\nSwarm Mode feature is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a parent agent with Swarm Mode enabled | Parent agent created with Swarm Mode toggle ON |
| 2 | Configure 2+ child agents with distinct tools and prompts (e.g., one with Jira toolkit, one with GitHub toolkit) | Child agents configured and associated with parent swarm agent |
| 3 | Open the parent agent chat and send a request that requires invocation of multiple child agents (e.g., 'Check Jira ticket ABC-123 and create a GitHub issue for it') | Chat request is submitted successfully |
| 4 | Observe the chat output for thought/action steps showing each child agent invocation | All relevant child agents are invoked; thought/action accordion shows execution for each child agent |
| 5 | Repeat the same request 3 times to verify consistency | All child agents are invoked consistently across all runs; no missing invocations |
| 6 | Send a request requiring only one specific child agent | Only the relevant child agent is invoked; response is correct and complete |

## Expected Final State

Only the relevant child agent is invoked; response is correct and complete

## Pass/Fail Criteria

All child agents invoked when relevant to the request\nConsistent behavior across 3+ identical runs\nThought/action accordion visible for each child agent execution\nNo missing or skipped child agent invocations
