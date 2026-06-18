---
id: ELITEA-0738
title: "Model Dropdown Performance and Functionality"
priority: medium
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0738: Model Dropdown Performance and Functionality

**Module:** Model Settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the dropdown remains smooth and functional with capability icons, and handles large model lists without performance issues.

**Coverage:**
- Dropdown opens promptly with large model lists (20+ models)
- Smooth scrolling through the model list
- Search functionality (if available) works correctly
- Model selection applies correctly
- No performance degradation with repeated open/close
- Consistent performance across Chat, Agents, and Pipelines

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has a large number of available models (20+)

## Test Data

- Test context: Chat with large model list
- Test models: any available models for selection
- Timing: dropdown should open within 1 second

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Verify the environment has 20+ models available. Open the model selector dropdown. | Dropdown opens within approximately 1 second. All models are listed with capability icons. |
| 2 | Scroll through the full model list from top to bottom using mouse wheel or scrollbar. | Scrolling is smooth with no stuttering or lag. All models and icons render correctly. |
| 3 | If a search field is present in the dropdown, type part of a model name (e.g., 'GPT'). | Model list filters correctly to show only matching models. |
| 4 | Clear the search field. Verify the full model list is displayed again. | All models reappear in the list. |
| 5 | Select a model from the list. Close the dropdown. | Model selection is applied. Selected model name is displayed. |
| 6 | Open the dropdown again. Verify the previously selected model is highlighted or indicated. | Selected model is visually indicated in the list. |
| 7 | Open and close the dropdown 5 times in quick succession. | Dropdown remains responsive. No noticeable performance degradation or slowdown. |
| 8 | Navigate to Agents. Open agent model configuration dropdown. Verify dropdown opens promptly and scrolls smoothly. | Performance is consistent in Agents context. |
| 9 | Navigate to Pipelines. Open LLM node model configuration dropdown. Verify dropdown opens promptly and scrolls smoothly. | Performance is consistent in Pipelines context. |

## Expected Final State

Performance is consistent in Pipelines context.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens within 1 second even with 20+ models
- Scrolling is smooth with no lag
- Search functionality (if present) filters correctly
- Model selection applies correctly
- No performance degradation with repeated open/close
- Consistent performance across Chat, Agents, and Pipelines

**Fail:**
- Dropdown takes longer than 2 seconds to open
- Scrolling is laggy or stutters
- Search does not filter correctly
- Model selection fails or does not apply
- Performance degrades noticeably after multiple opens
- Inconsistent performance across product areas
