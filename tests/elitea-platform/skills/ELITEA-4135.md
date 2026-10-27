---
id: ELITEA-4135
title: Verify admin can configure max_invoked_skills_per_turn to custom value
priority: High
objective: Verify that an admin can configure max_invoked_skills_per_turn to a custom value (e.g., 7) and the runtime enforces the new limit
preconditions: |
  - User is logged in as admin with configuration permissions
  - Access to admin configuration interface or config files
  - Agent exists with at least 8 different skills attached
  - User has access to chat with the agent
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "per-turn-limit", "S11", "configuration", "admin"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. As admin, navigate to the configuration interface (admin panel or config file)
2. Locate the max_invoked_skills_per_turn configuration setting
3. Change max_invoked_skills_per_turn from default (5) to custom value (7)
4. Save the configuration and restart services if required
5. Navigate to Chat and start a conversation with an agent that has at least 8 skills attached
6. Send a message invoking exactly 7 skills using ~skill syntax
7. Verify the message processes successfully
8. Send another message attempting to invoke 8 skills using ~skill syntax
9. Observe the system behavior

## Expected Results

- Admin can successfully change max_invoked_skills_per_turn configuration to 7
- Configuration is saved without errors
- After configuration change, messages with 7 skill invocations are processed successfully
- All 7 skills are executed in a single turn
- Messages attempting to invoke 8 skills (exceeding the new limit) are rejected or limited to 7 invocations
- Appropriate error or warning message is shown when limit is exceeded
