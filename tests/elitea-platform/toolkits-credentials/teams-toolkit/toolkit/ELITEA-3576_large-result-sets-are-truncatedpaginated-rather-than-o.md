---
id: ELITEA-3576
title: "Large Result Sets Are Truncated/Paginated Rather Than Overwhelming the Response"
priority: medium
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3576: Large Result Sets Are Truncated/Paginated Rather Than Overwhelming the Response

**Module:** Teams Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that read tools returning potentially large result sets (many teams, channels, chats, or messages) apply a sane limit/pagination instead of returning an unbounded payload.

## Preconditions

- Teams toolkit enabled with an authorized credential
- Access to a tenant/account with a large number of teams, chats, or messages in at least one channel/chat (or ability to simulate a high-volume scenario)

## Test Data

- N/A (scenario-based; use whatever high-volume tenant data is available)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `list_teams` or `list_chats` against an account with many teams/chats | Result is capped at a reasonable limit or paginated, not an unbounded dump |
| 2 | Call `find_chat_messages` or `search_teams_messages` against a channel/chat with a large message history | Result is capped at a reasonable limit or paginated, not an unbounded dump |

## Expected Final State

Both large-result calls return a bounded, well-formed result set.

## Pass/Fail Criteria

**Pass:**
- Both calls return a capped/paginated result set with no failure or excessive payload size

**Fail:**
- Either call returns an unbounded result, times out, or fails due to payload size
