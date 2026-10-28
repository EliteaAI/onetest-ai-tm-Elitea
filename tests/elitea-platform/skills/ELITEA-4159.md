---
id: ELITEA-4159
title: Verify removing skills from agent over limit allows adding new skills
priority: High
objective: Verify that when an agent is over the limit (e.g., 50/10), removing skills to get under the limit re-enables the "Add Skill" button
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with 50 skills attached
  - max_skills_per_agent is configured to 10
  - Agent skill counter shows "50/10"
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "limits", "S11", "ui-validation"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has 50 skills attached with limit of 10 (counter shows "50/10")
2. Verify "Add Skill" button is disabled
3. Remove 1 skill (agent now has 49 skills)
4. Check if "Add Skill" button is still disabled (should be, since 49 > 10)
5. Continue removing skills until exactly 10 remain
6. Verify counter shows "10/10"
7. Check "Add Skill" button state (should still be disabled at limit)
8. Remove 1 more skill (agent now has 9 skills)
9. Verify counter shows "9/10"
10. Check "Add Skill" button state
11. Attempt to attach a new skill

## Expected Results

- "Add Skill" button remains disabled while skill count exceeds limit (50, 49, ... 11, 10)
- When skill count drops below limit (to 9), "Add Skill" button becomes enabled
- Button no longer shows the "Maximum number of skills reached" tooltip when enabled
- Counter accurately reflects the count as skills are removed (50/10, 49/10, ... 9/10)
- At 9/10, user can successfully attach a new skill
- After attaching at 9/10, counter updates to 10/10 and button is disabled again
- UI state transitions are immediate and responsive
