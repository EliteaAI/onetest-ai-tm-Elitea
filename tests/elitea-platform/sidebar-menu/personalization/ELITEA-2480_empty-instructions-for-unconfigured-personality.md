---
id: ELITEA-2480
title: "Empty instructions for unconfigured personality"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2480: Empty instructions for unconfigured personality

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify empty text area displays when personality has no saved instructions

## Preconditions

- User logged in to Elitea application
- At least one personality (e.g., Quirky) has NO saved instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > AI Personality | |
| 2 | Select personality with no saved instructions (e.g., "Quirky") from Default persona dropdown | |
| 3 | Observe User instructions text area | |
| 4 | Verify text area is empty or shows placeholder text | |
| 5 | Verify placeholder text reads: "No custom instructions for the Quirky persona yet. Type here to add some." | |

## Expected Results

- User instructions text area is empty (no pre-filled text)
- Placeholder text indicates personality has no custom instructions yet
- Text area is editable and ready for input

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
