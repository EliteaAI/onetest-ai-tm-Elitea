---
id: ELITEA-0068
title: "Nested Sub-Participant Chain Executes Successfully [Parametrized: Sub-Agent → Sub-Agent | Sub-Pipeline → Sub-Pipeline]"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:pipelines, feat:agents, sub-agent, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0068: Nested Sub-Participant Chain Executes Successfully [Parametrized: Sub-Agent → Sub-Agent | Sub-Pipeline → Sub-Pipeline]

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that nested sub-participant chains work correctly — a sub-agent can invoke another sub-agent, and a sub-pipeline can invoke another sub-pipeline — with each level receiving context via `task` and completing successfully.

**Parameters:**
| # | Chain type |
|---|---|
| 1 | Sub-Agent → Sub-Agent (agent invokes a child agent which also invokes an agent) |
| 2 | Sub-Pipeline → Sub-Pipeline (pipeline invokes a child pipeline which invokes another pipeline) |

**Coverage (per parameter):**
- First-level sub-participant is invoked by the parent and receives `task`
- First-level sub-participant successfully invokes the next-level sub-participant
- Full chain completes and returns a result back up to the parent
- No errors at any level of the chain

## Preconditions

- Logged in to {{base_url}}
- **For sub-agent chain:** Agent A has Agent B as participant; Agent B has Agent C as participant
- **For sub-pipeline chain:** Pipeline A calls Pipeline B (Agent Node); Pipeline B calls Pipeline C (Agent Node)
- All participants are properly configured with valid instructions/tasks

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the top-level parent agent/pipeline and trigger a request that requires the full nested chain to execute | Parent begins execution and invokes level-1 sub-participant |
| 2 | Observe that level-1 sub-participant invokes level-2 sub-participant | The chain propagates — level-2 sub-participant is invoked and executes |
| 3 | Wait for the full chain to complete and inspect the final output at the top level | All levels complete successfully. Final output is returned to the top-level parent. No errors at any chain level. |
| 4 | Repeat steps 1–3 for the second parameter (switch between sub-agent chain and sub-pipeline chain) | Both chain types execute successfully end-to-end |

## Expected Final State

Both chain types execute successfully end-to-end

## Pass/Fail Criteria

**Pass:**
- All levels of the nested chain execute without error
- Each level passes context via `task` and receives a valid response
- The parent receives the final chained result

**Fail:**
- Any level of the chain fails or produces an error
- Context is not passed correctly between levels
- The chain breaks mid-execution
