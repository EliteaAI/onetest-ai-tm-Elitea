---
id: ELITEA-4843
title: "Enforce the chat starter limit on agent create, version create and MCP version update"
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
- The platform limit M is set to 5 (restore the original value at the end)
- An API token and access to the ELITEA MCP server are available

## Test Data

| Path | Request | Starters | Expected |
|------|---------|----------|----------|
| UI new agent | Agents → + Create | 5 | Saved with 5 |
| Create version | `POST {{base_url}}/api/v2/elitea_core/versions/prompt_lib/{{project_id}}/<app_id>` | 6 / 5 | 400 / 2xx |
| Create agent | `POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{{project_id}}` | 6 | 400, nothing created |
| MCP | `put_elitea_core_version` on the new agent | 5 / 6 | stored / rejected |
| Count rule | version update | 5 non-empty + `null` | accepted, 5 stored |
| Count rule | version update | 5 non-empty + `"   "` | 400 "cannot be empty or whitespace-only" (unchanged rule) |
| Limit error | — | — | "conversation_starters cannot exceed 5 items, got 6" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the create form for a new agent and scroll to Chat Starters | The counter reads "0/5 starters added." |
| 2 | Add 5 starters one by one | The counter goes from 1/5 to 5/5 |
| 3 | Hover + Starter at 5/5 | + Starter is disabled with the tooltip "You have reached the limit of chat starters" |
| 4 | Save the agent and reopen it | It is saved with 5 starters; the editor reads "5/5 starters added." |
| 5 | Send the create-version request with 6 starters, then with 5 | 6 → 400 on field `conversation_starters` with the limit error, and no version created; 5 → 2xx |
| 6 | Send the create-agent request with 6 starters | 400 with the limit error; no agent is created |
| 7 | Call MCP `put_elitea_core_version` on the new agent with 5 starters, then with 6 | 5 is stored; 6 is rejected with the limit error and the stored 5 are unchanged |
| 8 | Update the version with 5 starters plus `null` | Accepted; `null` is dropped and 5 starters are stored |
| 9 | Update the version with 5 starters plus `"   "` | Rejected by the whitespace-only rule, which is unchanged, not by the limit |
| 10 | Delete the new agent and restore the original limit | Cleaned up |

## Expected Final State

Every authoring path enforces M. No agent or version with more than 5 starters was created.

## Pass/Fail Criteria

**Pass:**
- The UI stops at M, and every API and MCP request above M returns 400 with the limit error and changes nothing
- Requests at or below M succeed; `null` items aren't counted

**Fail:**
- Any path stores more than M starters for a new version, or rejects a request at M
- The error message doesn't name the limit and the count
