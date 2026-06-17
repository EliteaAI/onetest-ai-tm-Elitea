---
id: ELITEA-0927
title: "Verify Adding a Pipeline or Agent as a Chat Participant — Creation Flow"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0927: Verify Adding a Pipeline or Agent as a Chat Participant — Creation Flow

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that creating a new Pipeline or Agent directly as a chat participant functions correctly after the pipeline UX refactor.

**Coverage:**
- Creating a new pipeline via the chat participant creation flow
- Creating a new agent via the chat participant creation flow

## Preconditions

- Logged in
- Private project selected
- A chat conversation is open (or can be created)

## Test Data

- Pipeline participant Name: TC16-Chat-Pipeline-Participant
- Agent participant Name: TC16-Chat-Agent-Participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Chat interface is displayed |
| 2 | Open the participant management panel | Panel for adding/managing participants opens |
| 3 | Select 'Create new Pipeline' (or equivalent option) | Pipeline creation form opens within the chat context |
| 4 | Enter Name (TC16-Chat-Pipeline-Participant) and Description | Fields are populated |
| 5 | Click Save | Pipeline is saved. The pipeline is added as a participant |
| 6 | Open participant management panel again | Panel opens |
| 7 | Select 'Create new Agent' (or equivalent option) | Agent creation form opens within the chat context |
| 8 | Enter Name (TC16-Chat-Agent-Participant) and Description | Fields are populated |
| 9 | Click Save | Agent is saved. The agent is added as a participant |

## Expected Final State

Agent is saved. The agent is added as a participant

## Pass/Fail Criteria

**Pass:**
- Both pipeline and agent can be created via the chat participant flow without error
- Created participants appear in the conversation

**Fail:**
- Creation of a pipeline or agent as a chat participant fails
- The participant creation form does not open or save correctly within the chat context
