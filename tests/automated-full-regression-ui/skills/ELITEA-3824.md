---
id: ELITEA-3824
title: Verify disabled "Add Skill" button shows tooltip explaining maximum limit reached
priority: High
objective: Verify that the disabled "Add Skill" button displays a tooltip message "Maximum number of skills reached" when hovered
preconditions: |
  - User is logged in with agent creation/edit permissions
  - max_skills_per_agent is configured to default value (50)
  - Agent has exactly 50 skills attached
folder: Automated Full Regression UI/Skills
tags: ["skills", "agent-editor", "limits", "attach-limit", "S11", "ui-validation", "tooltip"]
status: Draft
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Agents section and open an agent that has exactly 50 skills attached
2. Verify the skill counter shows "50/50"
3. Verify the "Add Skill" button is disabled
4. Hover the mouse cursor over the disabled "Add Skill" button
5. Wait for the tooltip to appear (typically 500ms-1s delay)
6. Read the tooltip message

## Expected Results

- A tooltip appears when hovering over the disabled "Add Skill" button
- The tooltip displays the message "Maximum number of skills reached" or similar clear message
- The tooltip remains visible while hovering
- The tooltip disappears when moving the cursor away from the button
- The tooltip message clearly communicates why the button is disabled
