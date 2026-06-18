---
id: ELITEA-0733
title: "Model Dropdown Shows Capability Icons with Hover Tooltips"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0733: Model Dropdown Shows Capability Icons with Hover Tooltips

**Module:** Model Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify the model selection dropdown displays capability icons next to model names, and hovering shows tooltips with appropriate delay (2-3 seconds).

**Coverage:**
- Vision icon displayed next to Vision-capable models in dropdown
- Reasoning icon displayed next to Reasoning-capable models
- Multiple icons shown for models with multiple capabilities
- Tooltip appears on icon hover after 2-3 second delay
- Tooltip content correctly identifies the capability
- Tooltip disappears when cursor moves away
- Consistent behavior across Chat, Agents, and Pipelines

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has models with varying capabilities

## Test Data

- Vision-capable models: GPT-4 Vision, Claude 3 Opus
- Reasoning-capable models: Claude 3.5 Sonnet
- Models with multiple capabilities: GPT-4 Vision, Claude 3 Opus

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open the model selector dropdown. | Dropdown displays a list of available models. |
| 2 | Scan through the model list. Locate a Vision-capable model (e.g., GPT-4 Vision). | Vision/eye icon is displayed next to the model name. |
| 3 | Locate a Reasoning-capable model in the list (e.g., Claude 3.5 Sonnet). | Reasoning icon is displayed next to the model name. |
| 4 | Locate a model with multiple capabilities (e.g., Claude 3 Opus). | Multiple icons (Vision + Reasoning) are displayed next to the model name. |
| 5 | Hover the mouse cursor over a capability icon (e.g., Vision icon). Do not click. Hold hover for less than 1 second, then move away. | No tooltip appears during brief hover (< 1 second). |
| 6 | Hover the mouse cursor over the same capability icon again. Hold hover for 2-3 seconds. | Tooltip appears after approximately 2-3 seconds displaying the capability name (e.g., 'Image analysis'). |
| 7 | While tooltip is visible, move the cursor away from the icon. | Tooltip disappears immediately. |
| 8 | Hover over a different capability icon (e.g., Reasoning icon) and wait for tooltip. | Tooltip appears after 2-3 seconds displaying 'Reasoning' or equivalent description. |
| 9 | Navigate to Agents. Open agent model configuration dropdown. Verify capability icons are present for appropriate models. | Capability icons are displayed in Agents model dropdown. |
| 10 | Navigate to Pipelines. Open LLM node model configuration dropdown. Verify capability icons are present for appropriate models. | Capability icons are displayed in Pipelines LLM node dropdown. |

## Expected Final State

Capability icons are displayed in Pipelines LLM node dropdown.

## Pass/Fail Criteria

**Pass:**
- Capability icons are displayed next to appropriate models in dropdown
- Icons correctly represent model capabilities (Vision, Reasoning)
- Tooltip appears after 2-3 second hover delay
- Tooltip displays correct capability description
- Tooltip disappears when cursor moves away
- Behavior is consistent across Chat, Agents, and Pipelines

**Fail:**
- Capability icons are missing or incorrect
- Tooltip does not appear on hover
- Tooltip appears too quickly (< 1 second) or too slowly (> 5 seconds)
- Tooltip content is incorrect or missing
- Inconsistent behavior across different product areas
