---
id: ELITEA-4141
title: Verify forking agent with 50 skills keeps first 10 skills when limit is 10
priority: High
objective: Verify that forking an agent with 50 skills when limit is 10 keeps the first 10 skills and reports 40 warnings
preconditions: |
  - User is logged in with agent fork permissions
  - Agent exists with 50 skills attached in another project or as published
  - max_skills_per_agent is configured to 10
  - User has permission to fork agents
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "fork", "limits", "S11", "warnings"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. As admin, ensure max_skills_per_agent is set to 10
2. Navigate to an agent that has 50 skills attached (could be in another project or published)
3. Click "Fork" to create a copy in the current project
4. Review any warnings or messages displayed during fork operation
5. Complete the fork process
6. Open the forked agent in the agent editor
7. Count the number of skills attached to the forked agent
8. Verify which skills were kept (should be first 10)
9. Check fork logs or notifications for warnings about dropped skills
10. Compare the skill list with the original agent's first 10 skills

## Expected Results

- Fork operation completes successfully
- Exactly 10 skills are attached to the forked agent (the first 10 from the original 50)
- Skill counter displays "10/10"
- System reports 40 warnings indicating that 40 skills were excluded due to limit
- Warning message clearly explains which skills were not forked and why
- The 10 forked skills match the first 10 skills from the source agent
- Forked agent is functional with the 10 attached skills
- Original agent remains unchanged with all 50 skills
