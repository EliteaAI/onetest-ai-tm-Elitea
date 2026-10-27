---
id: ELITEA-4148
title: Verify bulk attach from Skill Hub respects remaining slots
priority: High
objective: Verify that bulk attaching multiple skills from Skill Hub to an agent respects the remaining available slots and provides appropriate feedback
preconditions: |
  - User is logged in with skill and agent edit permissions
  - Agent exists with 45 skills attached (5 slots remaining when limit is 50)
  - Skill Hub has at least 10 skills available to attach
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "skill-hub", "bulk-attach", "limits", "S11", "multi-select"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Skill Hub
2. Open the "Attach to Agent" dialog
3. Select the agent that has 45 skills attached (5 slots remaining)
4. Attempt to select 10 skills for bulk attachment
5. Observe any warnings or indicators about available slots
6. Confirm the bulk attach operation
7. Check the result notification or error message
8. Navigate to the agent editor
9. Verify the final skill count

## Expected Results

- UI shows remaining slots indicator (e.g., "5 slots remaining")
- When selecting more skills than available slots, a warning appears
- System either:
  - Prevents selecting more than 5 skills, OR
  - Allows selection but warns that only first 5 will be attached
- Bulk attach operation attaches only the first 5 skills (up to the limit)
- Clear feedback message explains that 5 skills were attached and 5 were skipped due to limit
- Agent ends up with exactly 50 skills (45 original + 5 newly attached)
- No skills beyond the limit are attached
