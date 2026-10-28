---
id: ELITEA-4147
title: Verify attempting to attach 51st skill returns 400 error with clear message
priority: High
objective: Verify that attempting to attach a 51st skill when limit is 50 returns HTTP 400 with a clear error message containing the configured maximum
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with exactly 50 skills attached
  - max_skills_per_agent is configured to 50
  - At least 1 additional skill exists to attempt attaching
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "limits", "error-handling", "S11", "negative-test"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has exactly 50 skills attached
2. Verify the skill counter displays "50/50"
3. Using API tools or by manipulating the UI (if button disable can be bypassed), attempt to attach a 51st skill
4. Capture the API response
5. Verify the HTTP status code
6. Read the error message in the response
7. Verify the error message content

## Expected Results

- API returns HTTP status code 400 (Bad Request)
- Error response body contains a clear error message
- Error message includes the configured maximum (e.g., "Cannot attach skill: agent has reached the maximum of 50 skills")
- Error message does not expose sensitive system information
- UI displays the error message to the user in a user-friendly way
- Agent's skill list remains at 50 skills (no partial attach)
- The attempted 51st skill is not added to the agent
