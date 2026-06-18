---
id: ELITEA-0932
title: "Context Not Injected into Multi-Level Sub-Agents, Swarm Children, or Sub-Pipelines"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, story:3395, sub-agent, pipeline, r-2.0.4, swarm]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0932: Context Not Injected into Multi-Level Sub-Agents, Swarm Children, or Sub-Pipelines

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that Project Context is not injected into sub-agents at multiple nesting levels, Swarm child agents, or sub-pipelines.

**Coverage:**
- 3-level agent chain: only master knows context
- Swarm mode: only parent orchestrator knows context, no crash
- Sub-pipeline called from master: does not know context

## Preconditions

- Master agent configured to call Sub-Agent A, which calls Sub-Agent B
- Master agent instructed to relay each level's response about the QA-TEST-PHRASE
- A Swarm-mode agent with child agents configured
- A sub-pipeline available for the master to call

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Iron bridge over the lake`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Iron bridge over the lake'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Run the master agent from the Agent page. Send: 'Ask all sub-agents (A and B) about the QA-TEST-PHRASE and relay their exact responses.' | Master agent knows the phrase. Sub-Agent A and Sub-Agent B both report they do not know 'Iron bridge over the lake'. |
| 3 | Enable Swarm mode on the parent agent (with child agents configured). Run the Swarm agent. Ask: 'What is the QA-TEST-PHRASE?' | Swarm executes without crash. The parent/orchestrator returns the phrase. Child agents within the Swarm do NOT know the phrase. |
| 4 | Configure the master agent to call a sub-pipeline. Ask the master to query the sub-pipeline about the QA-TEST-PHRASE and relay what it said. | Master reports the sub-pipeline does not know the phrase. Sub-pipeline context isolation holds. |

## Expected Final State

Master reports the sub-pipeline does not know the phrase. Sub-pipeline context isolation holds.

## Pass/Fail Criteria

**Pass:**
- Only master/parent at each level knows the phrase
- All sub-agents and sub-pipelines report not knowing it
- Swarm executes without error

**Fail:**
- Any sub-agent or sub-pipeline returns the phrase (isolation broken)
- Swarm crashes due to context injection
