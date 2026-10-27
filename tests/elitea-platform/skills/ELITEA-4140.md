---
id: ELITEA-4140
title: Verify importing agent with 50 skills keeps first 10 skills when limit is 10
priority: High
objective: Verify that importing a published agent with 50 skills when limit is 10 keeps the first 10 skills and reports 40 warnings
preconditions: |
  - User is logged in with agent import permissions
  - Published agent exists with 50 skills attached
  - max_skills_per_agent is configured to 10
  - User has access to import published agents
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "import", "limits", "S11", "warnings"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. As admin, ensure max_skills_per_agent is set to 10
2. Navigate to the published agents registry or marketplace
3. Find a published agent that has 50 skills attached
4. Click "Import" or "Fork" to import the agent into the current project
5. Review any warnings or messages displayed during import
6. Complete the import process
7. Open the imported agent in the agent editor
8. Count the number of skills attached to the imported agent
9. Verify which skills were kept (should be first 10 based on skill order)
10. Check import logs or notifications for warnings about dropped skills

## Expected Results

- Import operation completes successfully
- Exactly 10 skills are attached to the imported agent (the first 10 from the original 50)
- Skill counter displays "10/10"
- System reports 40 warnings indicating that 40 skills were excluded due to limit
- Warning message clearly explains which skills were dropped and why
- The 10 imported skills match the first 10 skills from the published agent (based on skill ID or attachment order)
- Imported agent is functional with the 10 attached skills
