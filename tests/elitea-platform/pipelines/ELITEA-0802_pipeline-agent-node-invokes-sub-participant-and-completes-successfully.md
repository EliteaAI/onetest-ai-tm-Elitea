---
id: ELITEA-0802
title: "Pipeline (Agent Node) Invokes Sub-Participant and Completes Successfully [Parametrized: Sub-Agent | Sub-Pipeline]"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipelines, feat:agents, sub-agent, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0802: Pipeline (Agent Node) Invokes Sub-Participant and Completes Successfully [Parametrized: Sub-Agent | Sub-Pipeline]

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a Pipeline with an Agent Node (configured to call an agent or another pipeline) correctly invokes the sub-participant, passes context via `task`, and completes the full pipeline execution successfully.

**Parameters:**
| # | Sub-participant type |
|---|---|
| 1 | Sub-Agent (Agent Node points to an Agent) |
| 2 | Sub-Pipeline (Agent Node points to a Pipeline) |

**Coverage (per parameter):**
- Pipeline with Agent Node runs end-to-end without error
- Agent Node invokes the sub-participant and receives a valid response
- Pipeline output reflects the sub-participant's result
- No `chat_history` passed into the sub-participant

## Preconditions

- Logged in to {{base_url}}
- **For Sub-Agent:** A pipeline containing an Agent Node configured to invoke an agent
- **For Sub-Pipeline:** A pipeline containing an Agent Node configured to invoke another pipeline
- Both sub-participants have a clear, testable task

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline from the Pipelines page and run it (provide required inputs if any) | Pipeline execution starts |
| 2 | Observe the Agent Node step — expand the thinking steps or node output chip to inspect what was sent to the sub-participant | The input shown in the thinking steps / Agent Node chip contains the delegated context (task). No `chat_history` is visible in the sub-participant input. |
| 3 | Wait for the full pipeline to complete and inspect the output | Pipeline completes successfully. Output contains the sub-participant's result. No errors in any node. |
| 4 | Repeat steps 1–3 for the second parameter (switch between Sub-Agent and Sub-Pipeline node targets) | Both parameter variants pass with the same behavior |

## Expected Final State

Both parameter variants pass with the same behavior

## Pass/Fail Criteria

**Pass:**
- Pipeline completes successfully for both parameter variants
- Agent Node returns valid output from the sub-participant
- Pipeline final output incorporates the sub-participant's result

**Fail:**
- Pipeline fails or Agent Node errors out
- Sub-participant returns no result or an error
- Pipeline output is empty or incorrect
