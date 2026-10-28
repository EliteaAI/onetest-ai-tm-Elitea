---
id: ELITEA-4156
title: Verify skill registry total size stays within budget with 50 skills
priority: High
objective: Verify that with 50 skills attached, the total skill registry stays within the configured size budget (approximately 16k chars / 4k tokens)
preconditions: |
  - User is logged in with chat access
  - Agent exists with exactly 50 skills attached
  - Skills have descriptions of varied lengths
  - Access to backend logs or debugging tools to inspect registry size
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "runtime", "performance", "registry-budget", "S11", "backend"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Attach exactly 50 skills to an agent, including some with descriptions near the 2304 character limit
2. Start a chat with the agent
3. Send a message to trigger registry generation
4. In backend logs, capture the <available_skills> registry content
5. Measure the total character count of the registry
6. Calculate or verify the approximate token count (characters / 4 for rough estimate)
7. Verify registry structure and that no skills are silently dropped
8. Count the number of skills listed in the registry

## Expected Results

- Registry contains all 50 skills (no skills are dropped)
- Total registry size is approximately 16k characters or less
- Approximate token count is around 4k tokens or less
- If individual skill descriptions are long, they are truncated evenly to fit within budget
- Registry truncation maintains fairness (no skill gets disproportionately truncated)
- Registry remains byte-stable and deterministic
- All skill names are fully visible (names are not truncated)
- Descriptions are truncated only if necessary to meet budget, with minimum floor (e.g., 120 chars)
