---
id: ELITEA-4155
title: Verify full skill description available when skill is invoked via ~skill
priority: High
objective: Verify that when a skill is invoked using ~skill syntax, the full skill body is loaded regardless of registry description truncation
preconditions: |
  - User is logged in with chat access
  - Agent exists with a skill attached that has description and body content
  - The skill has description longer than 512 characters
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "skill-invocation", "S11", "description-limit"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Create a skill with a description longer than 512 characters and complex body content (instructions, parameters, examples)
2. Attach the skill to an agent
3. Start a chat with the agent
4. Send a message that triggers the agent to invoke the skill using ~skill syntax
   - Example: "Please use ~<skill_name> to help me"
5. Observe backend logs or debugging tools to see what skill body is loaded
6. Verify that the full skill content is loaded when invoked
7. Verify the agent successfully executes the skill with full context

## Expected Results

- ~skill invocation triggers loading of the full skill body
- Complete skill description (all 1000+ characters) is loaded, not just the registry truncated version
- Full skill instructions, parameters, and examples are available to the agent
- Agent can successfully execute the skill with complete information
- Skill execution is not impaired by registry truncation
- Backend logs confirm full skill body was loaded for the invocation
