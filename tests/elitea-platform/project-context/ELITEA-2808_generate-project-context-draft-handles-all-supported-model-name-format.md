---
id: ELITEA-2808
title: "generate_project_context_draft handles all supported model_name formats without returning a bare empty response"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:generate_project_context_draft, model-compatibility]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2808: generate_project_context_draft handles all supported model_name formats without returning a bare empty response

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request template | `{"project_id": 13, "user_description": "Test with model <MODEL_NAME>", "llm_settings": {"model_name": "<MODEL_NAME>"}}` |
| Short model IDs | gpt-5.2, gpt-5.4, gpt-5.4-mini, gpt-5.6-luna, gpt-5.6-luna-2026-07-09, gpt-5-mini |
| Dated Bedrock IDs | eu.anthropic.claude-sonnet-4-5-20250929-v1:0, eu.anthropic.claude-sonnet-4-6, eu.anthropic.claude-haiku-4-5-20251001-v1:0 |
| Latest short Bedrock alias | eu.anthropic.claude-sonnet-5 |
| global.-prefixed IDs | global.anthropic.claude-sonnet-5, global.openai.gpt-5.6-luna, global.openai.gpt-5.6-sol, global.openai.gpt-5.6-terra |
| Display names | "Anthropic Claude Haiku 4.5", "Anthropic Claude 4.6 Sonnet" |
| Invalid model | nonexistent-model-xyz-999 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the request template once for each short model ID and each dated Bedrock ID (9 values total) | Each call returns a valid markdown draft |
| 2 | Run the request template with `eu.anthropic.claude-sonnet-5` and with `nonexistent-model-xyz-999` | Each call returns either a valid draft or a specific, actionable error — never a bare "empty response" |
| 3 | Run the request template with each `global.`-prefixed model_name (4 values) | Each call resolves to a valid draft, or returns a specific, actionable prefix-resolution error — never a bare "empty response" |
| 4 | Run the request template with each display-name value (2 values) | Each call is accepted and returns a valid draft, or returns a specific, actionable format error — never a bare "empty response" |

## Expected Final State

Every supported model_name format either produces a usable draft or a specific, actionable error; no format silently degrades to an unexplained "empty response".

## Pass/Fail Criteria

**Pass:**
- All 9 baseline model_name values return a valid draft
- Unresolvable/nonexistent model_name returns a clear "model not found" error rather than an empty response
- `global.`-prefixed and display-name values resolve to a draft or return a clear, specific error

**Fail:**
- Any valid model_name (in any supported format) returns "empty response" instead of a draft
- An invalid model_name returns "empty response" instead of a clear not-found error
