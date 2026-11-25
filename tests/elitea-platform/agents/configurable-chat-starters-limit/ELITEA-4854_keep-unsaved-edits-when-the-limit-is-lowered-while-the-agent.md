---
id: ELITEA-4854
title: "Keep unsaved edits when the limit is lowered while the agent editor is open"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin in two browser contexts (A and B)
- The platform limit M is 10 (restore the original value at the end)
- An agent has 4 starters

## Test Data

| Field | Value |
|-------|-------|
| Limit change while editing | 10 → 3 |
| Expected error | "conversation_starters cannot exceed 4 items, got 5" |
| Unsaved edits | a changed welcome message or instructions, plus a 5th starter |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Context A: open the agent editor | The counter reads "4/10" |
| 2 | Context A: change the welcome message (or instructions) and add a 5th starter; don't save | The counter reads "5/10" |
| 3 | Context B: set the limit to 3 and Save | Saved |
| 4 | Context A: click Save | The save is rejected with an error toast showing the backend message from Test Data |
| 5 | Check the form | The changed text and the 5th starter are still in the form |
| 6 | Check the counter | It refreshes to "5/3" in the over-limit state |
| 7 | Delete the 5th starter and Save | The save succeeds with 4 starters and the text change stored |
| 8 | Restore the welcome message and the original limit | Cleaned up |

## Expected Final State

The rejected save lost nothing. The agent has 4 starters and the text edit.

## Pass/Fail Criteria

**Pass:**
- A clear error toast with the backend message; unsaved edits kept; counter refreshed to the new M

**Fail:**
- Edits are lost, there's a generic or no error, or the counter keeps the stale M
