---
id: ELITEA-4138
title: Verify "Save as version" copies all attached skills regardless of current limit
priority: High
objective: Verify that the "Save as version" operation copies all attached skills from the source agent version, even if the number exceeds the current configured limit
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with 50 skills attached
  - max_skills_per_agent is currently set to 10 (lower than attached skills)
  - User has permission to create new versions
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "versioning", "S11", "data-integrity", "save-as-version"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has 50 skills attached (skill counter shows "50/10")
2. Click "Save as version" or similar version creation option
3. Provide a new version name/number
4. Confirm the version creation
5. Wait for the operation to complete
6. Navigate to the newly created version
7. Count the number of skills attached to the new version
8. Verify the skill counter display
9. Compare the skill list in the new version with the original version

## Expected Results

- "Save as version" operation completes successfully
- The new version is created with all 50 skills copied from the original
- Skill counter in the new version displays "50/10"
- All 50 skills from the original version are present in the new version
- No skills are dropped or excluded during the copy operation
- The new version maintains the same skill order and configuration
- No errors or warnings about exceeding the limit during version creation
