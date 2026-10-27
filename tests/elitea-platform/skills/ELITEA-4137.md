---
id: ELITEA-4137
title: Verify agent with 50 skills shows "50/10" when limit is lowered to 10
priority: High
objective: Verify that when max_skills_per_agent is lowered (e.g., from 50 to 10), an agent with 50 attached skills displays the over-limit count (50/10) in the editor without removing skills
preconditions: |
  - User is logged in as admin with configuration permissions
  - Agent exists with exactly 50 skills attached
  - max_skills_per_agent is initially set to 50
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "limits", "configuration", "S11", "data-integrity", "admin"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Create or open an agent with exactly 50 skills attached (with limit set to 50)
2. Verify the skill counter shows "50/50"
3. As admin, change max_skills_per_agent configuration from 50 to 10
4. Save the configuration and restart services if required
5. Navigate back to the agent editor and open the same agent
6. Check the skill counter display
7. Verify all 50 skills are still listed in the attached skills section
8. Attempt to attach an additional (51st) skill
9. Attempt to save the agent without making changes

## Expected Results

- After limit is lowered to 10, the skill counter displays "50/10" indicating the agent has 50 skills but the limit is now 10
- All 50 skills remain attached and visible in the skills list
- No skills are automatically removed when the limit is lowered
- "Add Skill" button is disabled because the agent exceeds the new limit
- User cannot attach additional skills while at 50/10
- Agent can still be saved without errors (existing over-limit skills are preserved)
- Agent continues to function normally in chat with all 50 skills available
