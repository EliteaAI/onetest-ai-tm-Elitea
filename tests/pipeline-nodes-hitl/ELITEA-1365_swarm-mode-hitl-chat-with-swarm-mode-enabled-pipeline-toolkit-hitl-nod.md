---
id: ELITEA-1365
title: "[Swarm Mode + HITL] Chat with Swarm Mode Enabled — Pipeline Toolkit HITL Node Shows Approve/Reject Buttons"
priority: critical
type: functional
module: pipeline-nodes-hitl
status: ready
execution_type: manual
tags: [feat:swarm-mode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5065]
---
# ELITEA-1365: [Swarm Mode + HITL] Chat with Swarm Mode Enabled — Pipeline Toolkit HITL Node Shows Approve/Reject Buttons

**Module:** Pipeline Nodes Hitl · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when Chat is configured with Swarm mode enabled and executes a pipeline toolkit containing a HITL node, the approval buttons are shown and functional.

**Coverage:**
- Pipeline executed as a toolkit from a Swarm-mode-enabled Chat
- HITL node surfaces Approve and Reject buttons correctly in Chat context
- Pipeline resumes after Reject decision
- Confirms the bug affects Chat context as well as Agent context

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A pipeline exists that includes a HITL node
- Chat is configured with Swarm mode ENABLED and the above pipeline added as a participant/toolkit
- Browser: Chrome latest

## Test Data

- Chat: Swarm mode ON, pipeline toolkit attached
- Pipeline: contains at least 1 HITL node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open a conversation with the Swarm-mode-enabled configuration. | Chat loads. |
| 2 | Send a message that triggers the pipeline toolkit execution. | Pipeline begins executing. |
| 3 | Wait for the pipeline to reach the HITL node. | Pipeline pauses at the HITL step. |
| 4 | Observe the chat interface at the HITL pause point. | Approve and Reject buttons are visible and interactive. |
| 5 | Click Reject. | Pipeline resumes and completes the Reject route successfully. |

## Expected Final State

Pipeline resumes and completes the Reject route successfully.

## Pass/Fail Criteria

**Pass:**
- HITL buttons visible in Chat context
- Pipeline resumes and completes after clicking Reject

**Fail:**
- No buttons appear; pipeline stuck; user cannot proceed
