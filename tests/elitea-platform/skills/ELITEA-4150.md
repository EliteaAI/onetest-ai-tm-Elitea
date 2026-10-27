---
id: ELITEA-4150
title: Verify skill counter accuracy as skills are added and removed
priority: High
objective: Verify that the skill counter displays accurate count as skills are added and removed from an agent
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with 0 skills attached
  - At least 10 skills are available to attach
  - max_skills_per_agent is set to 50
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "ui", "counter", "S11", "usability"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent with 0 skills attached
2. Verify the skill counter displays "0/50"
3. Attach one skill
4. Verify the counter updates to "1/50"
5. Attach 4 more skills (total 5)
6. Verify the counter displays "5/50"
7. Remove 2 skills (leaving 3)
8. Verify the counter displays "3/50"
9. Attach 7 more skills (total 10)
10. Verify the counter displays "10/50"
11. Save the agent and reopen it
12. Verify the counter still shows "10/50" after reload

## Expected Results

- Counter starts at "0/50" for agent with no skills
- Counter updates immediately when a skill is attached (no page refresh needed)
- Counter updates immediately when a skill is removed
- Counter shows accurate format: "current/maximum"
- Counter displays correct numbers after every add/remove operation
- Counter persists correctly after save and reload
- Counter updates are consistent across all views (editor, preview, etc.)
