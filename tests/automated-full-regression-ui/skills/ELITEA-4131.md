---
id: ELITEA-4131
title: Verify agent can attach exactly 50 skills (default limit)
priority: High
objective: Verify that an agent can attach exactly 50 skills when the default limit is configured to 50
preconditions: |
  - User is logged in with agent creation/edit permissions
  - At least 50 skills exist in the project or public registry
  - max_skills_per_agent is configured to default value (50)
folder: Automated Full Regression UI/Skills
tags: ["skills", "agent-editor", "limits", "attach-limit", "S11", "positive-test"]
status: Draft
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Agents section and create a new agent or open an existing agent in the editor
2. Click "Add Skills" button to open the skill picker
3. Select and attach skills one by one, counting as you attach
4. Continue attaching skills until exactly 50 skills are attached to the agent
5. Verify the skill counter displays "50/50" or "50 of 50"
6. Attempt to save the agent

## Expected Results

- Each skill attaches successfully up to the 50th skill
- The skill counter accurately displays the current number of attached skills (1/50, 2/50, ... 50/50)
- All 50 attached skills are visible in the agent's skill list
- The agent saves successfully with all 50 skills attached
- After save, reopening the agent shows all 50 skills still attached
