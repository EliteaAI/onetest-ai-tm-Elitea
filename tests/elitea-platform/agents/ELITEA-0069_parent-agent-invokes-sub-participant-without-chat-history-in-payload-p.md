---
id: ELITEA-0069
title: "Parent Agent Invokes Sub-Participant Without chat_history in Payload [Parametrized: Sub-Agent | Sub-Pipeline]"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, sub-agent, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0069: Parent Agent Invokes Sub-Participant Without chat_history in Payload [Parametrized: Sub-Agent | Sub-Pipeline]

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a parent agent delegates work to a sub-participant (either a sub-agent or a sub-pipeline), the sub-participant receives all required context through the `task` field only — with no `chat_history` included in the request payload — and completes successfully.

**Parameters:**
| # | Sub-participant type |
|---|---|
| 1 | Sub-Agent (agent added as participant) |
| 2 | Sub-Pipeline (pipeline added as participant) |

**Coverage (per parameter):**
- Parent agent invokes the sub-participant and passes context via `task` field
- Sub-participant request payload contains no `chat_history`
- Sub-participant completes its task and returns a result to the parent
- Parent agent incorporates the result into its final response
- No errors or missing context during delegation

## Preconditions

- Logged in to {{base_url}}
- **For Sub-Agent:** A parent agent configured with a child agent added as a participant
- **For Sub-Pipeline:** A parent agent configured with a pipeline added as a participant
- The sub-participant has a clear, testable task (e.g., summarize provided text)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the parent agent from the Agents page and navigate to its Test Settings panel | Agent test interface is loaded |
| 2 | Send a request that triggers the parent agent to delegate work to the sub-participant (e.g., 'Summarize this text using the sub-agent/sub-pipeline: [sample text]') | Parent agent begins processing and invokes the sub-participant |
| 3 | In the agent run output, expand the thinking steps and inspect the toolkit/participant chip that shows what was sent to the sub-participant | The input shown in the thinking steps contains the delegated context (task). No `chat_history` is visible in the sub-participant input shown in the chip. |
| 4 | Wait for the sub-participant to complete and observe the parent agent's final response | Sub-participant returns a valid result. Parent agent produces a coherent final response. No errors are shown. |
| 5 | Repeat steps 1–4 for the second parameter (switch between Sub-Agent and Sub-Pipeline) | Both parameter variants pass with the same behavior |

## Expected Final State

Both parameter variants pass with the same behavior

## Pass/Fail Criteria

**Pass:**
- Sub-participant executes and returns a valid result for both parameter variants
- Network payload contains `task` but no `chat_history` in both cases
- Parent agent's final response reflects the sub-participant's output

**Fail:**
- Sub-participant fails due to missing context
- `chat_history` is present in the sub-participant request payload
- Parent agent returns an error or incomplete response
