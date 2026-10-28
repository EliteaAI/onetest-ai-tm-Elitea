---
id: ELITEA-4146
title: Verify individual skill descriptions are limited to 2304 characters in registry
priority: High
objective: Verify that skill descriptions in the agent skill registry are limited to 2304 characters to maintain performance
preconditions: |
  - User is logged in with skill creation permissions
  - Agent exists with at least one attached skill
  - Access to skill editor or skill description field
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "skill-registry", "limits", "S11", "performance", "description-limit"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Create a new skill or open an existing skill in the skill editor
2. Navigate to the skill description field
3. Paste or type a description that is exactly 2304 characters long
4. Save the skill
5. Attach the skill to an agent
6. Open the agent in chat and invoke the agent (to load the skill registry)
7. In backend logs or developer tools, verify the skill registry payload
8. Check that the skill description in the registry is at most 2304 characters
9. Create another skill with a description longer than 2304 characters (e.g., 3000 characters)
10. Attach it to the agent and verify the registry again

## Expected Results

- Skills can be created with descriptions up to 2304 characters
- When a skill with 2304-character description is added to registry, the full description is included
- When a skill has a description longer than 2304 characters, the registry truncates or truncates it to 2304 characters
- The truncation is done cleanly (e.g., at word boundary, with ellipsis if truncated)
- The full skill description is still available when the skill is loaded via load_skill or ~skill
- The skill registry payload stays within the configured size budget with 50 skills
- Agent performance is not degraded with skills having maximum-length descriptions
