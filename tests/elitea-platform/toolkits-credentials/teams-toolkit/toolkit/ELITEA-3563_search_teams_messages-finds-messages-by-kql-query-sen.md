---
id: ELITEA-3563
title: "search_teams_messages — Finds Messages by KQL Query, Sender, and Date Across Chats/Channels"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3563: search_teams_messages — Finds Messages by KQL Query, Sender, and Date Across Chats/Channels

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `search_teams_messages` searches across the user's chats and channels and returns correctly scoped results, and rejects a criteria-less call.

## Preconditions

- Teams toolkit with `search_teams_messages` enabled, linked to an authorized credential
- Known message text present in both a chat and a channel, from a known sender, with a known older message available

## Test Data

| Variant | query | senders | since | Expected |
|---|---|---|---|---|
| A | matches known text | — | — | Matching chat and channel hits returned |
| B | — | known sender's email | — | Only that sender's messages |
| C | — | — | after a known older message | Older message excluded |
| D | — | — | — | Rejected with a "provide criteria" error |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `search_teams_messages` with Variant A | Matching messages from both a chat (`chatId`) and a channel (`teamId`/`channelId`) are returned |
| 2 | Invoke `search_teams_messages` with Variant B | Only the specified sender's messages are returned |
| 3 | Invoke `search_teams_messages` with Variant C | The known older message is excluded from results |
| 4 | Invoke `search_teams_messages` with Variant D (no `query`, `senders`, or `since`) | Call fails with a clear "provide criteria" error rather than returning unfiltered results |

## Expected Final State

Search results are correctly scoped by query/sender/date, and a criteria-less call never returns unfiltered data.

## Pass/Fail Criteria

**Pass:**
- All three positive filters scope results correctly; the criteria-less call is rejected

**Fail:**
- Any filter fails to scope results correctly, or a criteria-less call silently returns unfiltered results
