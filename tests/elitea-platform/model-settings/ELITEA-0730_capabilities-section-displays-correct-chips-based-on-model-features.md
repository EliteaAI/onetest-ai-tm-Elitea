---
id: ELITEA-0730
title: "Capabilities Section Displays Correct Chips Based on Model Features"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0730: Capabilities Section Displays Correct Chips Based on Model Features

**Module:** Model Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify the new "Capabilities" section correctly displays capability chips (Image analysis, Reasoning) based on each model's supported features, and updates dynamically when switching models.

**Coverage:**
- "Image analysis" chip appears for Vision-capable models
- "Image analysis" chip does not appear for non-Vision models
- "Reasoning" chip appears for Reasoning-capable models
- Both chips appear when model supports both capabilities
- Capabilities update immediately when switching models without modal close/reopen
- Consistent behavior across Chat, Agents, and Pipelines contexts

## Preconditions

- Logged into {{base_url}}
- User has access to model settings modal
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has models with varying capabilities

## Test Data

- Vision-capable models: GPT-4 Vision, Claude 3 Opus
- Non-Vision models: GPT-3.5-turbo
- Reasoning-capable models: Claude 3.5 Sonnet, GPT-4
- Models with both: GPT-4 Vision, Claude 3 Opus

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open the model selector dropdown. Select GPT-4 Vision. | Model settings modal opens. 'Image analysis' chip is displayed in the Capabilities section. |
| 2 | Without closing the modal, select GPT-3.5-turbo from the model list. | 'Image analysis' chip disappears immediately. Capabilities section shows no chips or is hidden. |
| 3 | Without closing the modal, select a Reasoning-capable model (e.g., Claude 3.5 Sonnet). | 'Reasoning' chip appears in the Capabilities section. |
| 4 | Without closing the modal, select a model with both Vision and Reasoning (e.g., Claude 3 Opus). | Both 'Image analysis' and 'Reasoning' chips are displayed simultaneously. |
| 5 | Switch between 3-5 different models without closing modal. | Capabilities chips update immediately each time with no lag or incorrect display. |
| 6 | Navigate to Agents. Open agent model configuration. Repeat steps 1-5 for agent context. | Capabilities section behaves identically in Agents context. |
| 7 | Navigate to Pipelines. Open an LLM node's model configuration. Repeat capability verification for at least 2 different models. | Capabilities section behaves identically in Pipelines LLM node context. |

## Expected Final State

Capabilities section behaves identically in Pipelines LLM node context.

## Pass/Fail Criteria

**Pass:**
- "Image analysis" chip appears only for Vision-capable models
- "Reasoning" chip appears only for Reasoning-capable models
- Both chips appear when model supports both
- Capabilities update immediately when switching models
- Behavior is consistent across Chat, Agents, and Pipelines

**Fail:**
- Incorrect capability chips shown for any model
- Chips do not update when switching models
- Chips appear for models that do not support the capability
- Behavior is inconsistent across different product areas
