---
id: ELITEA-4847
title: "Keep up to 10 chat starters when importing JSON and Markdown above the limit"
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
- Agents with 8 and 10 starters were exported from the UI (agent actions → Export) as JSON and as Markdown (`.agent.md`)
- The platform limit M is set to 3 (restore the original value at the end)

## Test Data

| Import file | Agents inside | Expected after import |
|-------------|---------------|-----------------------|
| JSON export | 8-starter agent, 10-starter agent | 8 and 10 in order, "8/3" and "10/3" |
| Markdown export | 8-starter agent | 8 in order, "8/3" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Import the JSON file through Agents → Import | Success dialog; both agents created; no limit error |
| 2 | Open both imported agents | 8 and 10 starters in source order; counters "8/3" and "10/3" in the over-limit state |
| 3 | On the 10-starter agent, hover + Starter | Disabled with the over-limit tooltip |
| 4 | Edit one starter and Save | The save at 10 succeeds |
| 5 | Delete one starter and Save | The save at 9 succeeds; the editor reads "9/3" |
| 6 | Send a version update back to 10 starters | 400 (the ceiling is now 9) |
| 7 | Import the Markdown file and open the imported agent | Success; 8 starters in source order; "8/3" |
| 8 | Delete the imported agents and restore the original limit | Cleaned up |

## Expected Final State

Imports keep up to 10 starters whatever M is. Imported versions then follow the lowered-limit rules.

## Pass/Fail Criteria

**Pass:**
- JSON and Markdown imports keep every starter (≤ 10) in order with no limit error
- The imported over-limit version can be saved at or below its stored count but not above it

**Fail:**
- An import is rejected or trimmed to M
- Order is lost, or the imported version can grow past its stored count
