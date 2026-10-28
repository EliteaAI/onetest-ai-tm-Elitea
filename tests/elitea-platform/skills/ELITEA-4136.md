---
id: ELITEA-4136
title: Verify existing agents with attached skills continue working after limit update
priority: High
objective: Verify backward compatibility - existing agents with attached skills (created before limit increase) continue to function correctly after the system is updated with new limit
preconditions: |
  - System exists with old skill limit (e.g., 5)
  - At least one agent exists with 5 skills attached (created before update)
  - System is updated with new max_skills_per_agent limit (50)
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "backward-compatibility", "S11", "data-integrity"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Before system update: Create an agent with 5 skills attached using the old limit
2. Note the skill IDs and names attached to the agent
3. Perform system update that raises max_skills_per_agent to 50
4. After update, navigate to the agent editor and open the agent created in step 1
5. Verify all 5 skills are still attached and displayed correctly
6. Navigate to Chat and send a message to the agent to invoke one of the attached skills
7. Verify the skill executes successfully
8. In the agent editor, attempt to attach additional skills (up to the new limit of 50)
9. Save the agent with additional skills

## Expected Results

- After system update, the agent still shows all 5 originally attached skills
- No skills are lost or corrupted during the update
- Skill counter displays correct count (e.g., "5/50" after update)
- All original skills are functional and can be invoked in chat
- User can attach additional skills up to the new limit (50 total)
- Agent saves successfully with both original and newly attached skills
- No data migration errors or warnings appear
