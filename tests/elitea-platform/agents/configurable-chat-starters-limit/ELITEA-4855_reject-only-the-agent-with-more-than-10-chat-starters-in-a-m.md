---
id: ELITEA-4855
title: "Reject only the agent with more than 10 chat starters in a mixed import"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A JSON export file has been edited by hand to hold agent A with 11 starters and agent B with 3 starters
- Neither agent exists in {{project_id}}

## Test Data

| Agent in file | Starters | Expected |
|---------------|----------|----------|
| A | 11 | Not created; error names A with "conversation_starters cannot exceed 10 items, got 11" |
| B | 3 | Imported with its 3 starters |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Agents → Import and select the mixed JSON file | The import runs |
| 2 | Look at the import result | A partial-result state (not the success dialog, not a generic failure); the error is shown on agent A with the message from Test Data |
| 3 | Search the Agents list for A | A doesn't exist |
| 4 | Open B | B exists with its 3 starters |
| 5 | Delete B | Cleaned up |

## Expected Final State

Only the valid agent was imported. The over-limit agent got a named, per-item error.

## Pass/Fail Criteria

**Pass:**
- Per-agent failure with the named error; the valid agent is imported

**Fail:**
- The whole import fails, A is created or trimmed, or the error doesn't say which agent failed
