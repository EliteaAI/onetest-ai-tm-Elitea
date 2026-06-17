---
id: ELITEA-0515
title: "Scrolling Down in Conversations Sidebar Loads the Next Batch [Parametrized: Today / This Week / Older]"
priority: critical
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [eng:technical-debt, nfr:usability, eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4834, EliteaAI/elitea_issues#4996]
---
# ELITEA-0515: Scrolling Down in Conversations Sidebar Loads the Next Batch [Parametrized: Today / This Week / Older]

**Module:** Chat Conversations Lazy Loading · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that scrolling to the bottom of a date group section triggers a new API batch request for that group, and new conversations are appended.

**Coverage:**
- Scroll in any date group fires a follow-up request with incremented `offset`
- New conversations are appended (not replacing existing ones)
- Tested across all three sections: Today, This Week, Older

## Preconditions

- Logged in to {{base_url}} in a project with more conversations than the first batch shows in each group
- DevTools → Network → Filter: `conversations`

## Test Data

| Section | Required |
|---------|----------|
| Today | More conversations today than the initial batch limit |
| This Week | More conversations this week than the initial batch limit |
| Older | More conversations older than this week than the initial batch limit |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Note initial `offset` and `limit` values from the first request. | Initial batch is loaded. |
| 2 | In the Today section, scroll to the bottom until more conversations are needed. | A new API request fires with `offset` = previous `offset + limit`. New conversations append below. |
| 3 | Repeat for the This Week section. | New request fires with incremented offset. Conversations appended. |
| 4 | Repeat for the Older section. | New request fires with incremented offset. Conversations appended. |

## Expected Final State

New request fires with incremented offset. Conversations appended.

## Pass/Fail Criteria

**Pass:**
- Each scroll triggers a new request with correctly incremented `offset`
- New conversations appear below existing ones without disruption

**Fail:**
- No request fires on scroll
- Offset does not increment
- Existing conversations disappear or reshuffle on append
