---
id: ELITEA-4845
title: "Keep existing chat starters when the limit is lowered from 10 to 5 and raised again"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- An agent was saved with 8 chat starters while M = 10
- The platform limit is then set to M = 5 (restore the original value at the end)

## Test Data

| Field | Value |
|-------|-------|
| Version update API | `PUT {{base_url}}/api/v2/elitea_core/version/prompt_lib/{{project_id}}/<app_id>/<version_id>` (or the editor Save) |
| Ceiling for a version | the larger of M and its stored starter count |
| Limits used | 10 → 5 → 10 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent editor | The counter reads "8/5" in the over-limit state; all 8 are listed |
| 2 | Edit only the instructions (no starter change) and Save | 2xx; 8 starters stored |
| 3 | Replace the text of starter #3 and Save | 2xx; 8 starters stored with the new text for #3 |
| 4 | Send a version update with 9 starters | 400 "conversation_starters cannot exceed 8 items, got 9" |
| 5 | Open a new chat with the agent as participant and expand the starters list | All 8 are reachable ("Show 4 more" shows the 8 saved starters in order) |
| 6 | In the editor, delete starters until 5 remain and Save | The counter reads "5/5" in the normal colour (`data-over-limit` false); the save succeeds |
| 7 | Hover + Starter | The normal at-limit tooltip "You have reached the limit of chat starters" is shown |
| 8 | Send a version update with 6 starters | 400 "conversation_starters cannot exceed 5 items, got 6" |
| 9 | Set M = 10 and reopen the editor | The counter reads "5/10"; + Starter is enabled |
| 10 | Add a 6th starter and Save | The save succeeds with 6 starters |
| 11 | Reset the agent to 8 starters (at M = 10) and restore the original limit | Cleaned up |

## Expected Final State

A version keeps its starters when M is lowered. It can never grow past the larger of M and its stored count, and it follows a raised M at once.

## Pass/Fail Criteria

**Pass:**
- Saves at or below the stored count succeed after M is lowered; going above it returns 400
- After the version is reduced to M the normal rules apply; raising M allows adding again

**Fail:**
- Lowering M deletes or blocks saving existing starters
- A version can grow past the larger of M and its stored count, or the counter doesn't leave the over-limit state at 5/5
