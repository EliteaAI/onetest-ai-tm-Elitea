---
id: ELITEA-4178
title: "Verify reasoning slider displays correct scale based on selected model (3 or 5 point)"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Project has multiple reasoning models available with different reasoning scales
- User has permission to create skills

## Test Data

| Model Type | Reasoning Scale | Expected Labels |
|------------|----------------|-----------------|
| 3-point reasoning model | 3 points | Low, Medium, High |
| 5-point reasoning model | 5 points | Off, Low, Medium, High, Extra High |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Create new skill | Skill editor opens |
| 2 | Expand "Run settings" accordion | Run settings section displays |
| 3 | Click Model selector → Select a 3-point reasoning model | Model selected |
| 4 | Click settings icon next to model | Model settings dialog opens |
| 5 | Observe REASONING slider labels | Slider displays: Low, Medium, High (3 points) |
| 6 | Verify slider has exactly 3 positions | Slider constrained to 3 points |
| 7 | Click "Cancel" → Return to model selector | Dialog closed |
| 8 | Select a 5-point reasoning model | Model changed |
| 9 | Click settings icon next to model | Model settings dialog opens |
| 10 | Observe REASONING slider labels | Slider displays: Off, Low, Medium, High, Extra High (5 points) |
| 11 | Verify slider has exactly 5 positions | Slider constrained to 5 points |
| 12 | Set slider to "Extra High" → Click "Apply" | Setting saved |
| 13 | Save skill → Reload page → Open Model settings | Settings persisted correctly with 5-point scale |

## Expected Final State

- Reasoning slider adapts to the selected model's capability
- 3-point models show 3 options only
- 5-point models show 5 options including "Off" and "Extra High"
- Selected reasoning level is saved and persists correctly

## Pass/Fail Criteria

**Pass:**
- 3-point models display Low/Medium/High only
- 5-point models display Off/Low/Medium/High/Extra High
- Slider UI reflects the correct scale for each model
- Saved reasoning level persists correctly

**Fail:**
- Slider shows incorrect number of options for model type
- Labels are incorrect or missing
- Cannot save reasoning level for 5-point model
- Reasoning scale does not adapt to model change
