---
id: ELITEA-4842
title: "Deliver the admin chat starter limit to the agent editor in a team project"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin who is a member of a team project
- The team project has an agent with K chat starters (K ≤ 6)
- The platform limit M is 6 (restore the original value at the end)

## Test Data

| Field | Value |
|-------|-------|
| Agent editor | `{{base_url}}/app/<team_project_id>/agents/all/<agent_id>` |
| Delivered value API | `GET {{base_url}}/api/v2/elitea_core/platform_settings/prompt_lib?project_id=<team_project_id>` |
| Limits used | M = 6, then M = 8 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent editor in the team project and scroll to Chat Starters | The counter reads "K/6 starters added." |
| 2 | Call the delivered value API for the team project | 200 with `conversation_starters_max: 6` |
| 3 | In Admin → Features → Chat Starters set the value to 8 and Save | Saved |
| 4 | Open the team-project agent editor again | The counter reads "K/8 starters added." (not a hardcoded 4 or 6) |
| 5 | Call the delivered value API for the team project | 200 with `conversation_starters_max: 8` |
| 6 | Restore the original limit | Restored |

## Expected Final State

The team project uses the platform-wide limit. The limit is back at its original value.

## Pass/Fail Criteria

**Pass:**
- The editor counter and `platform_settings` in the team project always match the admin value

**Fail:**
- The team project shows a hardcoded or stale limit, or the API returns an error or a non-integer value
