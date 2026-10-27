---
id: ELITEA-4152
title: Verify skill registry remains byte-stable between turns for prompt caching
priority: High
objective: Verify that the skill registry maintains byte stability between turns to ensure prompt cache hits and consistent performance
preconditions: |
  - User is logged in with chat access
  - Agent exists with 50 skills attached
  - Access to backend logs or debugging tools to inspect prompt payloads
  - Prompt caching is enabled in the system
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "performance", "prompt-caching", "S11", "backend"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Start a chat conversation with an agent that has 50 skills attached
2. Send the first message to the agent
3. Capture the skill registry payload from backend logs (the <available_skills> section in the prompt)
4. Note the exact byte sequence or hash of the registry
5. Send a second message in the same conversation
6. Capture the skill registry payload again
7. Compare the two registry payloads byte-by-byte
8. Send a third message and repeat the comparison
9. Verify prompt cache statistics (cache hits) in backend logs

## Expected Results

- Skill registry payload is identical (byte-for-byte) across all turns in the conversation
- Skills are listed in consistent order (sorted by skill_id, name) in every turn
- Skill descriptions are formatted identically in each turn
- No whitespace or formatting variations between turns
- Prompt cache logs show cache hits for the system prefix containing the skill registry
- No cache misses due to registry variations
- Registry remains stable even after agent invokes skills or performs actions
