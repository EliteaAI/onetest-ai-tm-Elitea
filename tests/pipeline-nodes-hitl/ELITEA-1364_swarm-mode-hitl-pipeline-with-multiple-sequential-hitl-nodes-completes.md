---
id: ELITEA-1364
title: "[Swarm Mode + HITL] Pipeline with Multiple Sequential HITL Nodes Completes All Approval Steps When Swarm Mode Is Enabled For Agent"
priority: high
type: functional
module: pipeline-nodes-hitl
status: ready
execution_type: manual
tags: [feat:swarm-mode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5065]
---
# ELITEA-1364: [Swarm Mode + HITL] Pipeline with Multiple Sequential HITL Nodes Completes All Approval Steps When Swarm Mode Is Enabled For Agent

**Module:** Pipeline Nodes Hitl · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline has multiple sequential HITL nodes, all approval steps are surfaced and completable when executed from a Swarm-mode-enabled agent.

**Coverage:**
- Pipeline with 2+ sequential HITL nodes executed in Swarm mode
- Each HITL node surfaces its buttons after the previous decision
- Pipeline completes all HITL steps and finishes execution

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A pipeline exists with 2 or more HITL nodes in sequence
- An agent with Swarm mode ENABLED has this pipeline as a toolkit
- Browser: Chrome latest

## Test Data

- Pipeline: 2 sequential HITL nodes, both with Approve and Reject routes
- Agent: Swarm mode ON

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent with Swarm mode ON and trigger the pipeline toolkit execution. | Pipeline starts executing. |
| 2 | Wait for the pipeline to reach the first HITL node. | Pipeline pauses; Approve and Reject buttons are visible. |
| 3 | Click Approve on the first HITL node. | Pipeline resumes and advances toward the second HITL node. |
| 4 | Wait for the pipeline to reach the second HITL node. | Pipeline pauses again; Approve and Reject buttons are visible for the second HITL. |
| 5 | Click Approve on the second HITL node. | Pipeline resumes and completes successfully. |

## Expected Final State

Pipeline resumes and completes successfully.

## Pass/Fail Criteria

**Pass:**
- All HITL nodes in the pipeline surface their buttons and are completable when Swarm mode is enabled
- Pipeline reaches and completes final state

**Fail:**
- Pipeline gets stuck at any HITL node when Swarm mode is on; buttons not shown for one or more nodes
