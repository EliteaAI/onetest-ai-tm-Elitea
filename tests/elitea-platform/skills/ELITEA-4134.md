---
id: ELITEA-4134
title: Verify agent can reference up to 5 ~skill invocations per message by default
priority: High
objective: Verify that an agent can invoke up to 5 skills per turn using ~skill syntax when max_invoked_skills_per_turn is set to default value (5)
preconditions: |
  - User is logged in with chat access
  - Agent exists with at least 5 different skills attached
  - max_invoked_skills_per_turn is configured to default value (5)
  - User has access to chat with the agent
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "per-turn-limit", "S11", "skill-invocation"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Navigate to Chat and start a conversation with an agent that has at least 5 different skills attached
2. In a single message, use ~skill syntax to invoke exactly 5 different skills
   - Example: "Please run ~skill1, ~skill2, ~skill3, ~skill4, and ~skill5"
3. Send the message
4. Wait for the agent to process and respond
5. Verify all 5 skills were invoked by checking the response or skill execution logs
6. Check for any error messages or warnings in the response

## Expected Results

- The message is accepted and processed
- All 5 skills referenced with ~skill syntax are successfully invoked during the turn
- The agent response shows results from all 5 skill invocations
- No error messages about exceeding skill invocation limits appear
- The turn completes successfully with all 5 skills executed
