---
id: ELITEA-1367
title: "[Swarm Mode + HITL] Agent with Swarm Mode Enabled — Pipeline Toolkit HITL Node Shows Approve/Reject Buttons"
priority: critical
type: functional
module: pipeline-nodes-hitl
status: ready
execution_type: manual
tags: [feat:swarm-mode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5065]
---
# ELITEA-1367: [Swarm Mode + HITL] Agent with Swarm Mode Enabled — Pipeline Toolkit HITL Node Shows Approve/Reject Buttons

**Module:** Pipeline Nodes Hitl · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when an agent with Swarm mode enabled executes a pipeline toolkit containing a HITL node, the HITL approval buttons (Approve/Reject) are displayed to the user and the pipeline does not get stuck.

**Coverage:**
- Pipeline executed as a toolkit from a Swarm-mode-enabled agent
- HITL node surfaces Approve and Reject buttons correctly
- Pipeline resumes after user decision
- Core bug scenario: stuck at HITL step when Swarm mode is ON

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A pipeline exists that includes a HITL node with Approve and Reject routes configured
- An agent exists with Swarm mode ENABLED and the above pipeline added as a toolkit
- Browser: Chrome latest

## Test Data

- Agent: Swarm mode ON, pipeline toolkit attached
- Pipeline: contains at least 1 HITL node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open the agent with Swarm mode enabled. | Agent chat view opens. |
| 2 | Send a message that triggers the pipeline toolkit execution. | Pipeline begins executing. |
| 3 | Wait for the pipeline to reach the HITL node. | Pipeline pauses at the HITL step. |
| 4 | Observe the chat interface at the HITL pause point. | Approve and Reject buttons (and Edit if configured) are visible and interactive. |
| 5 | Click Approve. | Pipeline resumes and completes the Approve route successfully. |

## Expected Final State

Pipeline resumes and completes the Approve route successfully.

## Pass/Fail Criteria

**Pass:**
- HITL buttons are visible and clickable
- Pipeline resumes and completes after clicking Approve

**Fail:**
- No buttons appear; pipeline is stuck with no way to proceed
