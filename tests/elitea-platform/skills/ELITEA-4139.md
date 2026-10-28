---
id: ELITEA-4139
title: Verify publishing agent with 50 skills copies all skills even if limit is lowered
priority: High
objective: Verify that publishing an agent copies all 50 attached skills to the published version, even when the current limit is lower than 50
preconditions: |
  - User is logged in with agent publish permissions
  - Agent exists with 50 skills attached
  - max_skills_per_agent is set to 10 (lower than attached skills)
  - User has permission to publish agents
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "publishing", "S11", "data-integrity"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has 50 skills attached (skill counter shows "50/10")
2. Click "Publish" or navigate to the publish workflow
3. Fill in required publish information (name, description, visibility, etc.)
4. Confirm and submit the publish operation
5. Wait for the publishing process to complete
6. Navigate to the published agent in the public registry or published agents list
7. Open the published agent to view its details
8. Count the number of skills attached to the published agent
9. Verify all 50 skills from the original agent are present

## Expected Results

- Publish operation completes successfully without timeout or errors
- All 50 skills are copied to the published agent
- Published agent shows all 50 skills in its skill list
- No skills are dropped during the publishing process
- Each of the 50 skills is properly forked/copied as a published version
- Published agent can be imported or forked by other users with all 50 skills
- No error messages about skill limits during publishing
