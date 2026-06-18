---
id: ELITEA-1363
title: "[Swarm Mode + HITL] All HITL Routes (Approve / Reject / Edit) Are Functional When Swarm Mode Is Enabled"
priority: high
type: functional
module: pipeline-nodes-hitl
status: ready
execution_type: manual
tags: [feat:swarm-mode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5065]
---
# ELITEA-1363: [Swarm Mode + HITL] All HITL Routes (Approve / Reject / Edit) Are Functional When Swarm Mode Is Enabled

**Module:** Pipeline Nodes Hitl · **Priority:** High · **Type:** Functional

**Objective:** Verify that all three HITL decision routes work correctly when triggered from an agent with Swarm mode enabled — not just that the buttons appear, but that each route correctly resumes the pipeline on its configured path.

**Coverage:**
- Approve route resumes pipeline on the correct branch
- Reject route resumes pipeline on the correct branch
- Edit route accepts input and resumes pipeline on the correct branch
- All three verified in Swarm mode context

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A pipeline exists with a HITL node that has all three routes configured: Approve, Reject, and Edit
- An agent with Swarm mode ENABLED has this pipeline as a toolkit
- Run the test three times, selecting a different decision each time

## Test Data

- Run A: Click Approve
- Run B: Click Reject
- Run C: Click Edit (submit edited input if required)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent with Swarm mode ON and trigger the pipeline toolkit execution. | Pipeline executes and pauses at the HITL node. |
| 2 | Verify all configured buttons (Approve, Reject, Edit) are visible in the chat interface. | All three buttons are displayed. |
| 3 | Click the decision for the current run: Run A — Approve / Run B — Reject / Run C — Edit. | Selected action is accepted by the system. |
| 4 | Observe pipeline continuation. | Pipeline resumes on the correct route for the chosen decision. |
| 5 | Confirm the pipeline completes on the expected branch. | Output or next node matches the configured route for the selected decision. |

## Expected Final State

Output or next node matches the configured route for the selected decision.

## Pass/Fail Criteria

**Pass:**
- All three routes (Approve/Reject/Edit) correctly resume the pipeline on their configured paths when Swarm mode is enabled

**Fail:**
- Any route button is missing, non-functional, or pipeline does not resume on the correct branch
