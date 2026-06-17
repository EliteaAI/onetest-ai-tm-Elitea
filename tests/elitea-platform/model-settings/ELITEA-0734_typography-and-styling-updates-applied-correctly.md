---
id: ELITEA-0734
title: "Typography and Styling Updates Applied Correctly"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:image-generation, feat:settings, eng:frontend, issue:4357, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4357]
---
# ELITEA-0734: Typography and Styling Updates Applied Correctly

**Module:** Model Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify "Reasoning" and "Creativity" labels display in uppercase, and dropdown text styling meets specification (14px font, appropriate colors per theme).

**Coverage:**
- "Reasoning" label displays as "REASONING" (uppercase)
- "Creativity" label displays as "CREATIVITY" (uppercase)
- Dropdown text is appropriately sized (approximately 14px)
- Dark theme: text is white/light colored, icons are light gray
- Light theme: text is dark, icons are medium gray
- Consistent styling across Chat, Agents, and Pipelines

## Preconditions

- Logged into {{base_url}}
- Browser: Chrome/Firefox/Edge (latest)
- Browser supports both light and dark themes

## Test Data

- Test models: any model with Reasoning and/or Creativity sliders
- Browser theme toggle location: Settings or system preference

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open model selector. Select a model that has Reasoning and Creativity settings visible. | Model settings modal opens with Reasoning and Creativity controls. |
| 2 | Locate the 'Reasoning' slider or setting label. | Label displays as 'REASONING' in all uppercase letters. |
| 3 | Locate the 'Creativity' slider or setting label. | Label displays as 'CREATIVITY' in all uppercase letters. |
| 4 | Open the model dropdown list. Observe the text size of model names in the dropdown. | Text appears appropriately sized (approximately 14px) and is easily readable. |
| 5 | Ensure dark theme is active. Open the model dropdown. Observe text and icon colors. | Model names are white or light colored. Capability icons are light gray. Text is readable with good contrast. |
| 6 | Switch to light theme (via browser settings or system preference). Open the model dropdown again. | Model names are dark colored. Capability icons are medium gray. Text is readable with good contrast. |
| 7 | Navigate to Agents. Open agent model configuration. Verify 'REASONING' and 'CREATIVITY' labels are uppercase. | Labels are uppercase in Agents context. |
| 8 | Navigate to Pipelines. Open LLM node model configuration. Verify dropdown styling in both themes. | Text and icon colors are appropriate for the active theme in Pipelines context. |

## Expected Final State

Text and icon colors are appropriate for the active theme in Pipelines context.

## Pass/Fail Criteria

**Pass:**
- "Reasoning" and "Creativity" labels are displayed in uppercase
- Dropdown text is appropriately sized and readable
- Dark theme: text is light colored, icons are light gray
- Light theme: text is dark colored, icons are medium gray
- Styling is consistent across Chat, Agents, and Pipelines

**Fail:**
- Labels are not in uppercase
- Text size is too small or too large, affecting readability
- Colors do not provide sufficient contrast in either theme
- Styling is inconsistent across different product areas
