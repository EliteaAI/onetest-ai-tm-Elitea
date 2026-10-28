---
id: ELITEA-4186
title: "Verify 3-point reasoning model displays slider with Low, Medium, High labels only"
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
- A 3-point reasoning model is available in the project (e.g., older Claude model)
- User has permission to create skills

## Test Data

| Field | Value |
|-------|-------|
| Model | 3-point reasoning model |
| Expected labels | Low, Medium, High |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Create new skill | Skill editor opens |
| 2 | Expand "Run settings" accordion | Run settings section displays |
| 3 | Click Model selector → Select a 3-point reasoning model | Model selected |
| 4 | Click settings icon next to model | Model settings dialog opens |
| 5 | Observe REASONING slider | Slider displays exactly 3 positions with labels: Low, Medium, High |
| 6 | Verify no "Off" or "Extra High" options are present | Only 3 options visible |
| 7 | Drag slider to each position → Verify labels | Low → Medium → High (3 positions only) |
| 8 | Set slider to "High" → Click "Apply" → Save skill | Settings saved |
| 9 | Reload page → Open Model settings → Verify reasoning shows "High" | Reasoning persisted correctly |

## Expected Final State

- 3-point model displays 3-position slider only
- Labels are: Low, Medium, High
- No extra options (Off, Extra High) available
- Settings save and persist correctly

## Pass/Fail Criteria

**Pass:**
- Slider shows exactly 3 positions
- Labels are Low, Medium, High
- No additional options present
- Selected reasoning level saves correctly

**Fail:**
- Slider shows more or fewer than 3 positions
- Incorrect labels displayed
- "Off" or "Extra High" options appear
- Reasoning level does not save
