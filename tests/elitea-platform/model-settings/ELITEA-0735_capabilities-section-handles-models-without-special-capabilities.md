---
id: ELITEA-0735
title: "Capabilities Section Handles Models Without Special Capabilities"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0735: Capabilities Section Handles Models Without Special Capabilities

**Module:** Model Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify appropriate display when a model has no Vision, Reasoning, or other special capabilities.

**Coverage:**
- Capabilities section behavior for models with no special capabilities
- No UI layout issues or broken elements
- Section gracefully hidden, shows empty state, or displays with no chips
- Smooth transition when switching to capability-rich models

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has at least one basic model with no special capabilities

## Test Data

- Basic model with no capabilities: GPT-3.5-turbo
- Capability-rich model: GPT-4 Vision, Claude 3 Opus

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open model selector. Select a basic model with no special capabilities (e.g., GPT-3.5-turbo). | Model settings modal opens. Model is selected. |
| 2 | Look for the Capabilities section in the model settings modal. | One of the following: (a) Capabilities section is completely hidden, (b) Capabilities section shows an empty state message, (c) Capabilities section is visible but contains no capability chips. |
| 3 | Verify there are no UI layout issues: no broken spacing, no placeholder text, no overlapping elements. | UI is clean with no visual errors. Modal layout is intact. |
| 4 | Without closing the modal, switch to a capability-rich model (e.g., GPT-4 Vision). | Capabilities section appears (if it was hidden) or populates with capability chips. Transition is smooth. |
| 5 | Switch back to the basic model with no capabilities. | Capabilities section returns to its empty/hidden state. No errors or visual glitches. |
| 6 | Repeat verification in Agents context: open agent model configuration, select a basic model, observe Capabilities section. | Capabilities section behaves appropriately (hidden/empty) in Agents context. |
| 7 | Repeat verification in Pipelines context: open LLM node model configuration, select a basic model, observe Capabilities section. | Capabilities section behaves appropriately (hidden/empty) in Pipelines context. |

## Expected Final State

Capabilities section behaves appropriately (hidden/empty) in Pipelines context.

## Pass/Fail Criteria

**Pass:**
- Capabilities section gracefully handles models with no special capabilities
- Section is either hidden, shows empty state, or displays with no chips
- No UI layout issues or broken elements
- Smooth transition when switching between models with and without capabilities

**Fail:**
- Capabilities section shows incorrect or placeholder data for basic models
- UI layout is broken or has visual errors
- Section behavior is inconsistent across product areas
- Errors occur when switching between models
