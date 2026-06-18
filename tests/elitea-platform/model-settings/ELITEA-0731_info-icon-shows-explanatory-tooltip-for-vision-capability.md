---
id: ELITEA-0731
title: "Info Icon Shows Explanatory Tooltip for Vision Capability"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0731: Info Icon Shows Explanatory Tooltip for Vision Capability

**Module:** Model Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify an info icon next to the Vision capability displays a tooltip explaining Vision's purpose (image analysis, not generation).

**Coverage:**
- Info icon (ⓘ) is present next to Vision capability indicator
- Tooltip appears on hover or click
- Tooltip clearly explains Vision is for image analysis/reading
- Tooltip distinguishes Vision from Image Generation
- Tooltip is readable in both light and dark themes

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Test environment has at least one Vision-capable model

## Test Data

- Vision-capable model: GPT-4 Vision or Claude 3 Opus
- Expected tooltip content: mentions "analyzing images", "reading image content", "describing what is visible in an image"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open model selector. Select a Vision-capable model (e.g., GPT-4 Vision). | Model settings modal opens. 'Image analysis' chip is displayed in the Capabilities section. |
| 2 | Locate the info icon (ⓘ) next to the 'Image analysis' chip or Vision indicator. | Info icon is visible next to the Vision capability indicator. |
| 3 | Hover the mouse cursor over the info icon (do not click). Wait 1-2 seconds. | Tooltip appears displaying explanatory text about Vision capability. |
| 4 | Read the tooltip content. Verify it explains Vision is used for: analyzing images, reading image content, describing what is visible in images. | Tooltip content clearly states Vision is for image analysis and understanding. |
| 5 | Verify the tooltip explicitly distinguishes Vision from Image Generation (or does not mention generation in a way that could cause confusion). | Tooltip does not conflate Vision with Image Generation. It focuses on image analysis/reading. |
| 6 | Move the cursor away from the info icon. | Tooltip disappears. |
| 7 | Switch the browser to dark theme (if currently in light theme). Hover over the info icon again. | Tooltip appears and text is readable with sufficient contrast in dark theme. |
| 8 | Switch the browser to light theme (if currently in dark theme). Hover over the info icon again. | Tooltip appears and text is readable with sufficient contrast in light theme. |

## Expected Final State

Tooltip appears and text is readable with sufficient contrast in light theme.

## Pass/Fail Criteria

**Pass:**
- Info icon is present next to Vision capability indicator
- Tooltip appears on hover
- Tooltip clearly explains Vision is for analyzing/reading/describing images
- Tooltip distinguishes Vision from Image Generation
- Tooltip is readable in both light and dark themes

**Fail:**
- Info icon is missing
- Tooltip does not appear on hover
- Tooltip content is unclear or confusing
- Tooltip conflates Vision with Image Generation
- Tooltip is unreadable in either theme due to poor contrast
