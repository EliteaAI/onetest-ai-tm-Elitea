---
id: ELITEA-4237
title: "Skill Run Configuration — LLM Settings Precedence"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, configuration, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4237: Skill Run Configuration — LLM Settings Precedence

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that LLM settings follow correct precedence: request override → project default model.

**Coverage:**
- Request-level llm_settings override project defaults
- Project default model used when no override provided
- Model selection works correctly for skill execution

## Preconditions

- Logged in to {{base_url}}
- A skill with saved version exists in the project
- Project has default model configured (e.g., Claude Sonnet)
- Multiple models available in the project

## Test Data

- Skill: Own project skill with valid instructions
- Project default model: e.g., "claude-sonnet-4-5"
- Override model: e.g., "claude-opus-4-5" (different from default)
- User input: "Identify which model you are"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "Identify which model you are"}` (no llm_settings). | API returns HTTP 200 with response. |
| 2 | Verify response or usage logs indicate project default model was used. | Project default model (e.g., Sonnet) was used for execution. |
| 3 | Send POST request to same endpoint with body: `{"user_input": "Identify which model you are", "llm_settings": {"model_name": "claude-opus-4-5"}}`. | API returns HTTP 200 with response. |
| 4 | Verify response or usage logs indicate override model was used. | Override model (Opus) was used, not project default. |
| 5 | Compare token usage or response characteristics to confirm different models were used. | Different models produced different responses or token counts, confirming precedence works. |

## Expected Final State

Different models produced different responses confirming precedence works.

## Pass/Fail Criteria

**Pass:**
- Without override: project default model used
- With override: request-specified model used
- Precedence order respected
- Both executions succeed

**Fail:**
- Override ignored, always uses project default
- Wrong model used in either case
- Precedence order not respected
