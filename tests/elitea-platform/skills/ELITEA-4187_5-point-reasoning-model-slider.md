---
id: ELITEA-4187
title: "Verify 5-point reasoning model displays slider with Off, Low, Medium, High, Extra High labels"
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
- A 5-point reasoning model is available in the project (e.g., Claude Opus 4.5)
- User has permission to create skills

## Test Data

| Field | Value |
|-------|-------|
| Model | 5-point reasoning model (e.g., Claude Opus 4.5) |
| Expected labels | Off, Low, Medium, High, Extra High |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Create new skill | Skill editor opens |
| 2 | Expand "Run settings" accordion | Run settings section displays |
| 3 | Click Model selector → Select a 5-point reasoning model | Model selected |
| 4 | Click settings icon next to model | Model settings dialog opens |
| 5 | Observe REASONING slider | Slider displays exactly 5 positions with labels: Off, Low, Medium, High, Extra High |
| 6 | Drag slider through each position → Verify labels | Off → Low → Medium → High → Extra High (5 positions) |
| 7 | Set slider to "Extra High" → Click "Apply" → Save skill | Settings saved with Extra High |
| 8 | Reload page → Open Model settings → Verify reasoning shows "Extra High" | Reasoning: Extra High persisted |
| 9 | Change to "Off" → Save → Reload → Verify "Off" persisted | Reasoning: Off persisted |

## Expected Final State

- 5-point model displays 5-position slider
- All labels present: Off, Low, Medium, High, Extra High
- All positions save and persist correctly
- User can select any of the 5 levels

## Pass/Fail Criteria

**Pass:**
- Slider shows exactly 5 positions
- Labels are Off, Low, Medium, High, Extra High
- All levels selectable and save correctly
- Settings persist after reload

**Fail:**
- Slider shows fewer than 5 positions
- Labels are incorrect or missing
- Cannot select "Off" or "Extra High"
- Settings do not persist
