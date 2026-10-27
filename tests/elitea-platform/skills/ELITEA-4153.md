---
id: ELITEA-4153
title: Verify attempting to invoke 6 skills per turn with default limit returns error
priority: High
objective: Verify that attempting to invoke 6 skills in a single turn when max_invoked_skills_per_turn is 5 results in appropriate error or limiting behavior
preconditions: |
  - User is logged in with chat access
  - Agent exists with at least 6 different skills attached
  - max_invoked_skills_per_turn is set to default value (5)
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "per-turn-limit", "S11", "error-handling", "negative-test"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Chat and start a conversation with an agent that has at least 6 skills attached
2. Compose a message that references exactly 6 different skills using ~skill syntax
   - Example: "Please run ~skill1, ~skill2, ~skill3, ~skill4, ~skill5, and ~skill6"
3. Send the message
4. Wait for the agent to process the message
5. Observe the agent's response
6. Check for error messages or warnings
7. Verify which skills were actually invoked (check logs or response)

## Expected Results

- System detects that 6 skills were requested, exceeding the limit of 5
- One of the following behaviors occurs:
  - Error message is returned: "Cannot invoke more than 5 skills per turn"
  - Only the first 5 skills are invoked, with a warning about the 6th being skipped
  - Request is rejected before any skills are invoked
- Error message clearly states the limit (5 skills per turn)
- User receives clear feedback about the limitation
- System behavior is consistent and predictable
- No skills beyond the 5th are executed in the turn
