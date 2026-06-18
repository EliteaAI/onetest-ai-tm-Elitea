---
id: ELITEA-1366
title: "[Swarm Mode + HITL] HITL Approval Works Correctly Across Different LLM Models [Parametrized]"
priority: high
type: functional
module: pipeline-nodes-hitl
status: ready
execution_type: manual
tags: [feat:swarm-mode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5065]
---
# ELITEA-1366: [Swarm Mode + HITL] HITL Approval Works Correctly Across Different LLM Models [Parametrized]

**Module:** Pipeline Nodes Hitl · **Priority:** High · **Type:** Functional

**Objective:** Verify that the HITL node surfaces correctly and is completable when Swarm mode is enabled, regardless of the LLM model configured on the agent — covering GPT models without reasoning support, GPT models with reasoning, and Anthropic Claude.

**Coverage:**
- GPT-5.2 / GPT-5.4 (no reasoning support)
- GPT-5-mini (reasoning-capable)
- Claude Sonnet 4.5 or 4.6 (Anthropic)
- HITL buttons visible and functional across all model types in Swarm mode

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A pipeline exists with a HITL node (Approve/Reject configured)
- An agent with Swarm mode ENABLED has this pipeline as a toolkit
- Credentials available for GPT and Anthropic models
- Run the test three times, each time switching the agent LLM model

## Test Data

- Run A: GPT-5.2 or GPT-5.4 (no reasoning support)
- Run B: GPT-5-mini (reasoning-capable)
- Run C: Claude Sonnet 4.5 or Claude Sonnet 4.6 (Anthropic)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent with Swarm mode ON. Set the LLM model for the current run: Run A — GPT-5.2 or GPT-5.4 / Run B — GPT-5-mini / Run C — Claude Sonnet 4.5 or 4.6. Important: Change the LLM not only for the agent, but also for the pipeline. | Model is configured and saved. |
| 2 | Send a message that triggers the pipeline toolkit execution. | Pipeline begins executing under the selected model. |
| 3 | Wait for the pipeline to reach the HITL node. | Pipeline pauses at the HITL step. |
| 4 | Observe the chat interface at the HITL pause point. | Approve and Reject buttons are visible and interactive — regardless of which model is active. |
| 5 | Click Approve. | Pipeline resumes and completes successfully. |
| 6 | Repeat steps 1–5 for each remaining model variant. | All three model variants produce the same correct behavior. |

## Expected Final State

All three model variants produce the same correct behavior.

## Pass/Fail Criteria

**Pass:**
- HITL buttons appear and pipeline completes correctly across all 3 model variants (GPT-5.2/5.4, GPT-5-mini, Claude Sonnet 4.5/4.6)

**Fail:**
- HITL stuck or buttons missing with any specific model — indicating a model-specific regression in Swarm + HITL handling
