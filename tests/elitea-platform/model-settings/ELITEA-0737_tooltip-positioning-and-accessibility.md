---
id: ELITEA-0737
title: "Tooltip Positioning and Accessibility"
priority: medium
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0737: Tooltip Positioning and Accessibility

**Module:** Model Settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify tooltips are positioned correctly, remain readable on different screen sizes, and work with keyboard navigation.

**Coverage:**
- Tooltip appears fully visible without overflow
- Tooltip remains readable on smaller screen resolutions
- Tooltip is accessible via keyboard navigation
- Info icon is keyboard-accessible
- Capability icons in dropdown are keyboard-accessible
- All interactive elements respond to keyboard input

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has Vision-capable models

## Test Data

- Test resolutions: 1920x1080, 1366x768, or browser window resize
- Test model: GPT-4 Vision or Claude 3 Opus

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set browser resolution to 1920x1080 or full-screen. Navigate to Chat. Open model selector. Select a Vision-capable model. | Model settings modal opens with Capabilities section visible. |
| 2 | Hover over the info icon (ⓘ) next to the Vision capability. Observe tooltip positioning. | Tooltip appears fully visible without being cut off by modal boundaries. |
| 3 | Resize browser window to a smaller resolution (e.g., 1366x768) or use browser zoom. Hover over the info icon again. | Tooltip remains fully visible and readable. Text is not cut off. |
| 4 | Use keyboard navigation (Tab key) to navigate through the model settings modal. Focus on the info icon. | Info icon receives keyboard focus (visible focus indicator). |
| 5 | While info icon is focused, press Enter or Space key. | Tooltip appears, displaying the Vision capability explanation. |
| 6 | Press Tab to move focus away from the info icon. | Tooltip disappears. Focus moves to the next interactive element. |
| 7 | Open the model dropdown. Use keyboard (Arrow keys) to navigate through the model list. | Focus moves through models. Capability icons are visible and associated with the correct models. |
| 8 | Focus on a model with capability icons. Use Tab or appropriate key to focus on a capability icon. Press Enter or Space. | If capability icons are directly focusable, tooltip appears. Otherwise, tooltip appears on model selection or hover. |

## Expected Final State

If capability icons are directly focusable, tooltip appears. Otherwise, tooltip appears on model selection or hover.

## Pass/Fail Criteria

**Pass:**
- Tooltips appear fully visible without overflow on different screen sizes
- Tooltips remain readable when browser is resized
- Info icon is accessible via keyboard navigation
- Tooltip appears when info icon is activated with Enter/Space
- Model list is navigable via keyboard
- All interactive elements respond appropriately to keyboard input

**Fail:**
- Tooltip is cut off by modal boundaries
- Tooltip becomes unreadable on smaller screens
- Info icon cannot be focused or activated via keyboard
- Tooltip does not appear on keyboard activation
- Keyboard navigation is broken or inconsistent
