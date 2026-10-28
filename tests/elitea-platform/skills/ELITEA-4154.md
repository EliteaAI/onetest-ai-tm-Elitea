---
id: ELITEA-4154
title: Verify full skill description available when skill is loaded via load_skill
priority: High
objective: Verify that when a skill is loaded via load_skill command, the full skill description is provided regardless of registry truncation
preconditions: |
  - User is logged in with chat access
  - Agent exists with a skill attached that has a description longer than 512 characters (registry truncation threshold)
  - User knows the skill name to use with load_skill
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "load-skill", "S11", "description-limit"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Create a skill with a description that is 1000 characters long (exceeds registry truncation limit of 512)
2. Attach the skill to an agent
3. Start a chat with the agent
4. Send a message: "load_skill <skill_name>" where <skill_name> is the name of the skill created in step 1
5. Wait for the agent to load and display the skill information
6. Verify the description shown in the response
7. Count the characters or compare with the original description
8. Verify the full description is present, not truncated

## Expected Results

- load_skill command executes successfully
- The skill is loaded with complete information
- Full 1000-character description is displayed (not truncated to 512 characters)
- Description matches the original skill description exactly
- No "..." or truncation indicators in the description
- All skill details (parameters, examples, etc.) are also fully loaded
- User can see complete skill documentation when explicitly loading the skill
