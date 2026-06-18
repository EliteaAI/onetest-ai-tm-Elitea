---
id: ELITEA-0214
title: "Model Capability Icons Visible in LLM Dropdown"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0214: Model Capability Icons Visible in LLM Dropdown

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that capability icons (image analysis, reasoning) are displayed next to models that support them in the LLM model dropdown.

**Coverage:**
- Image analysis icon shown for supported models
- Reasoning icon shown for supported models
- Icons absent for models without that capability

## Preconditions

- Published agent is open in chat, model dropdown is accessible

## Test Data

Anthropic Claude 4.5 Sonnet: Image analysis + Reasoning icons
GPT-5 mini: Image analysis only
GPT-4.1: Image analysis only

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the model dropdown for a published agent. | Model list is displayed. |
| 2 | Observe Anthropic Claude 4.5 Sonnet — check for image analysis and reasoning icons. | Both icons visible. |
| 3 | Observe GPT-5 mini — check for image analysis icon only. | Only image icon visible; no reasoning icon. |
| 4 | Confirm models without image analysis show no icon for that capability. | Icons absent where not supported. |

## Expected Final State

Icons absent where not supported.

## Pass/Fail Criteria

**Pass:**
- Capability icons match the expected model capabilities
- No icons shown for capabilities a model does not support

**Fail:**
- No capability icons shown for any model
- Icons shown for capabilities a model does not support
