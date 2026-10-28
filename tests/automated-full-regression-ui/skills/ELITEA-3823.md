---
id: ELITEA-3823
title: Verify "Add Skill" button is disabled when agent reaches configured limit
priority: High
objective: Verify that the "Add Skill" button becomes disabled when the agent has reached the maximum configured skill limit
preconditions: |
  - User is logged in with agent creation/edit permissions
  - At least 51 skills exist in the project or public registry
  - max_skills_per_agent is configured to default value (50)
folder: Automated Full Regression UI/Skills
tags: ["skills", "agent-editor", "limits", "attach-limit", "S11", "ui-validation"]
status: Draft
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Agents section and create a new agent or open an existing agent
2. Attach exactly 50 skills to the agent using the skill picker
3. Verify the skill counter displays "50/50"
4. Observe the "Add Skill" button state
5. Attempt to click the "Add Skill" button
6. Try alternative methods to attach more skills (if any exist, such as drag-and-drop or bulk attach)

## Expected Results

- When 50 skills are attached, the "Add Skill" button becomes visually disabled (grayed out or shows disabled styling)
- The disabled "Add Skill" button does not respond to clicks
- No skill picker dialog opens when attempting to click the disabled button
- No other method allows attaching a 51st skill to the agent
- The skill counter displays "50/50" indicating the limit has been reached
