---
id: ELITEA-2757
title: "Unchecked suggestions are excluded from the final applied result"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent with Name "Test Agent" and Description "Test description" is open

## Test Data

| Field | Value |
|-------|-------|
| Agent Name (original) | Test Agent |
| Agent Description (original) | Test description |
| Prompt | General prompt requesting improvements to Name and Description |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent with Name "Test Agent" and Description "Test description" | Current values confirmed |
| 2 | Click "Edit with AI" and enter a general prompt | Prompt accepted |
| 3 | Generate the draft and wait for completion | Wizard renders with suggestions for General step |
| 4 | Navigate to the General step | Suggested Name and Description values are shown alongside current values |
| 5 | Uncheck the checkbox for the suggested Name change | The Name checkbox becomes unchecked |
| 6 | Keep the Description checkbox checked | The Description checkbox remains checked |
| 7 | Complete the wizard and apply changes | Modal closes without error |
| 8 | Verify the Agent's Name field | Name remains "Test Agent" (original value retained, unchanged) |
| 9 | Verify the Agent's Description field | Description was updated to the suggested value |

## Expected Final State

Only the Description field reflects the AI suggestion; the Name field retains its original value because its checkbox was unchecked.

## Pass/Fail Criteria

**Pass:**
- The unchecked field is not modified; the checked field is updated as suggested

**Fail:**
- The unchecked suggestion is applied anyway, or the checked suggestion fails to apply
