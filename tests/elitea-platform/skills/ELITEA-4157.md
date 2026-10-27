---
id: ELITEA-4157
title: Verify sub-agents use only their own skills, not parent agent skills
priority: High
objective: Verify that when a sub-agent is invoked, it uses only its own attached skills and does not inherit skills from the parent agent
preconditions: |
  - User is logged in with agent creation and chat access
  - Parent agent exists with 10 specific skills attached (Skill A1-A10)
  - Sub-agent exists with 5 different skills attached (Skill B1-B5)
  - Parent agent is configured to use the sub-agent
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "sub-agents", "agent-hierarchy", "S11", "skill-scope"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Create a parent agent with 10 skills attached (Skill A1 through A10)
2. Create a sub-agent with 5 different skills attached (Skill B1 through B5)
3. Configure the parent agent to invoke the sub-agent in certain scenarios
4. Start a chat with the parent agent
5. Send a message that triggers the parent agent to invoke the sub-agent
6. Monitor backend logs to see which skills are loaded for the sub-agent
7. Verify the sub-agent's skill registry contains only B1-B5
8. Attempt to have the sub-agent use one of the parent's skills (A1-A10) via ~skill syntax or load_skill
9. Verify the sub-agent cannot access parent skills

## Expected Results

- Sub-agent's skill registry contains only its own 5 skills (B1-B5)
- Sub-agent's registry does NOT include any of the parent's skills (A1-A10)
- Sub-agent can successfully invoke its own skills (B1-B5)
- If sub-agent attempts to use a parent skill, it receives "skill not found" error
- Parent agent can use its own skills (A1-A10) normally
- Skills are properly scoped to each agent independently
- No skill inheritance or leakage between parent and sub-agents
