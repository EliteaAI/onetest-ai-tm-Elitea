---
id: ELITEA-2810
title: "generate_skill_draft behaves consistently with generate_project_context_draft across the same model_name compatibility matrix"
priority: high
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, tool:generate_skill_draft, model-compatibility, cross-tool-consistency]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2810: generate_skill_draft behaves consistently with generate_project_context_draft across the same model_name compatibility matrix

## Preconditions

- Test project (project_id 13) is accessible
- The equivalent generate_project_context_draft model-compatibility matrix has been executed for comparison

## Test Data

| Field | Value |
|-------|-------|
| Request template | `{"project_id": 13, "user_description": "Test with model <MODEL_NAME>", "llm_settings": {"model_name": "<MODEL_NAME>"}}` |
| Baseline models expected to pass | gpt-5.2, gpt-5.4, gpt-5.4-mini, gpt-5.6-luna-2026-07-09, eu.anthropic.claude-sonnet-4-5-20250929-v1:0, eu.anthropic.claude-sonnet-4-6 |
| Models that must be cross-checked against the project-context tool | gpt-5-mini, eu.anthropic.claude-haiku-4-5-20251001-v1:0 |
| Latest short Bedrock alias / invalid model | eu.anthropic.claude-sonnet-5, nonexistent-model-xyz-999 |
| global.-prefixed IDs | global.anthropic.claude-sonnet-5, global.openai.gpt-5.6-luna, global.openai.gpt-5.6-sol, global.openai.gpt-5.6-terra |
| Display names | "Anthropic Claude Haiku 4.5", "Anthropic Claude 4.6 Sonnet" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the request template once for each of the 6 baseline models | Each call returns a valid JSON draft |
| 2 | Run the request template for `gpt-5-mini` and `eu.anthropic.claude-haiku-4-5-20251001-v1:0` | Each call returns a valid JSON draft; result is compared against the equivalent generate_project_context_draft call for the same model |
| 3 | Run the request template for `eu.anthropic.claude-sonnet-5` and `nonexistent-model-xyz-999` | Each call returns either a valid draft or a specific, actionable error — never a bare "empty response" |
| 4 | Run the request template for each `global.`-prefixed value and each display-name value | Each call resolves to a valid draft or returns a specific, actionable error — never a bare "empty response" |

## Expected Final State

generate_skill_draft handles every supported model_name format at least as well as generate_project_context_draft does for the same model; no model succeeds in one tool and silently fails in the other.

## Pass/Fail Criteria

**Pass:**
- All 6 baseline models return a valid draft
- gpt-5-mini and the Haiku 4.5 dated ID behave the same way (pass/fail) as they do in generate_project_context_draft
- No valid model_name returns "unparseable output" or a bare "empty response"
- Invalid model_name returns a clear "model not found" error

**Fail:**
- A model_name that succeeds in generate_project_context_draft fails (unparseable/empty) in generate_skill_draft
- Any valid model_name returns "empty response" or "unparseable output" instead of a usable draft
- An invalid model_name returns "empty response" instead of a clear not-found error
