---
id: ELITEA-3562
title: "Ambiguous or Unknown Team/Channel/Chat Names Produce Actionable Errors"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3562: Ambiguous or Unknown Team/Channel/Chat Names Produce Actionable Errors

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify name-resolution errors across the toolkit are specific and actionable rather than generic failures.

## Preconditions

- Teams toolkit enabled with an authorized credential
- Two teams sharing the same display name exist (or can be simulated); at least one team/channel/chat name close to, but not exactly matching, a real one

## Test Data

| Scenario | Tool | Expected Behavior |
|---|---|---|
| Two teams share the same display name | `list_channels` / `send_channel_message` | Error states the name is ambiguous and lists the candidate team IDs to use instead |
| Team name doesn't exist, but is close to a real one | `list_channels` / `send_channel_message` | Error suggests the closest matching real team name |
| Team name doesn't exist and has no close match | `list_channels` / `send_channel_message` | Error points to `list_teams` to look it up |
| Channel name doesn't exist within a valid team | `list_channels` result used in `send_channel_message` | Error points to `list_channels` to look it up, with a close-match suggestion if applicable |
| Chat topic/ID doesn't exist | `find_chat_messages` / `send_chat_message` | Error points to `list_chats`, with a close-match suggestion if applicable, and never suggests an internal raw thread ID as a name |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `list_channels` or `send_channel_message` with a team name shared by two teams | Error states ambiguity and lists candidate team IDs |
| 2 | Call the same tools with a near-miss team name | Error suggests the closest matching real team name |
| 3 | Call the same tools with a team name with no close match | Error points to `list_teams` |
| 4 | Call `send_channel_message` with a channel name not present in a valid team | Error points to `list_channels`, with a close-match suggestion if applicable |
| 5 | Call `find_chat_messages` or `send_chat_message` with a non-existent chat topic/ID | Error points to `list_chats`, with a close-match suggestion if applicable, and never surfaces a raw internal thread ID as a suggested name |

## Expected Final State

Every resolution failure across the five scenarios produces the specific, actionable error described.

## Pass/Fail Criteria

**Pass:**
- Each of the five scenarios produces exactly its documented, specific error

**Fail:**
- Any scenario degrades to a generic error, omits the actionable guidance, or leaks a raw internal ID as a suggested name
