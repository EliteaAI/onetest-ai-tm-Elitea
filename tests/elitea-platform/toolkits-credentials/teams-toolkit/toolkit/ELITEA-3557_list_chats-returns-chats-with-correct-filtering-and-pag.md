---
id: ELITEA-3557
title: "list_chats — Returns Chats With Correct Filtering and Pagination"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3557: list_chats — Returns Chats With Correct Filtering and Pagination

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `list_chats` lists the user's chats (1:1, group, meeting) most-recently-active first, and that its filters and `limit` work correctly.

## Preconditions

- Teams toolkit with `list_chats` enabled, linked to an authorized credential
- Test account has at least one 1:1 chat, one group chat, some with unread messages, and enough total chats to exceed a small `limit`

## Test Data

| Variant | Filter | Expected |
|---|---|---|
| A | none | All chats, most recently active first |
| B | `chat_type=oneOnOne` | Only 1:1 chats |
| C | `chat_type=group` | Only group chats |
| D | `unread_only=true` | Only chats with unread messages |
| E | `topic_contains` / `member` (email) | Only matching chats |
| F | `limit` below total chat count | Truncated result, `truncated: true` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `list_chats` with Variant A | Chats returned ordered by most recent activity, each with members and a last-message preview |
| 2 | Invoke `list_chats` with Variant B, then Variant C | Only chats of the requested type are returned in each case |
| 3 | Invoke `list_chats` with Variant D | Only chats with unread messages are returned |
| 4 | Invoke `list_chats` with Variant E (`topic_contains`, then `member`) | Results are correctly filtered by topic substring and by member respectively |
| 5 | Invoke `list_chats` with Variant F | Result is truncated and reports `truncated: true` |

## Expected Final State

All filter combinations and the truncation flag behave as documented; no filter returns unfiltered/incorrect data.

## Pass/Fail Criteria

**Pass:**
- Every filter variant returns exactly the expected subset; truncation is reported correctly

**Fail:**
- Any filter returns unfiltered or incorrect results, or truncation is silent/missing
