---
id: ELITEA-3702
title: "Verify Direct Chat Usage Is Not Misattributed to Agent & Pipeline Breakdowns"
priority: critical
type: regression
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6631, EliteaAI/elitea_issues#6574]
---

# ELITEA-3702: Verify Direct Chat Usage Is Not Misattributed to Agent & Pipeline Breakdowns

**Module:** Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify a plain Chat conversation with a bare LLM participant is reflected in Costs/Tokens by User and by Model, but not misattributed into Agent & Pipeline breakdowns, and that an actual Agent execution does appear there.

**Coverage:**
- Bare-chat call appears in By User/By Model, not in Agent & Pipeline breakdowns
- Real agent execution appears correctly in both

## Preconditions

- Admin/owner access to Analytics > Costs/Tokens
- Ability to start a bare-LLM chat and separately execute a real agent

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "What is the capital of France?" |
| Agent | Any simple existing agent |
| Agent input | "Say hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a new Chat, add only an LLM participant (no agent/pipeline), send the test message | Model responds |
| 2 | Open Analytics > Costs and > Tokens for that window | Call appears in "Cost by User"/"Cost by Model" and "Token Usage by User"/"by Model" |
| 3 | Check "Cost by Agent & Pipeline" / "Token Usage by Agent & Pipeline" for the same window | No entry attributed to any agent/pipeline for this call |
| 4 | Execute the test Agent once with the test input | Agent responds |
| 5 | Reload Analytics > Costs and > Tokens for the same window | Agent's cost/tokens now populate "Cost by Agent & Pipeline"/"Token Usage by Agent & Pipeline" with the correct agent name |
| 6 | Check "Cost by User"/"by Model" for the agent call | Agent call's cost/tokens also appear there, alongside the bare-chat call |

## Expected Final State

Bare chat usage appears only in By User/By Model breakdowns, never in Agent & Pipeline breakdowns; actual agent executions appear correctly in both.

## Pass/Fail Criteria

**Pass:**
- Bare chat call: present in By User/By Model, absent from Agent & Pipeline breakdowns
- Agent call: present in both Agent & Pipeline breakdowns (correct agent name) and By User/By Model

**Fail:**
- Bare chat call appears under any agent/pipeline name
- Agent call is missing from Agent & Pipeline breakdowns
