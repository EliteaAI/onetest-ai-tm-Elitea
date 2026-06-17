---
id: ELITEA-0518
title: "Chat Sidebar Loads Conversations in Small Batches, Not All at Once"
priority: critical
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [eng:technical-debt, nfr:usability, eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4834]
---
# ELITEA-0518: Chat Sidebar Loads Conversations in Small Batches, Not All at Once

**Module:** Chat Conversations Lazy Loading · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that opening the Chat page triggers a paginated API request with a small `limit` (≤ 10-100) — not a single bulk request.

**Coverage:**
- `limit` parameter in conversation API requests is ≤ 10-100
- `offset` parameter is present (pagination is active)
- Date group sections (Today / Yesterday / This Week / Older) render correctly

## Preconditions

- Logged in to {{base_url}} in a team project with conversations in multiple date groups
- Browser DevTools available

## Test Data

- Any project with 30+ conversations distributed across Today, This Week, and Older groups
- DevTools → Network tab → Filter: `conversations`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open DevTools → Network tab. Filter by Fetch/XHR. | DevTools ready to capture requests. |
| 2 | Navigate to Chat in the sidebar. | Conversation list loads. Date group headers (Today / This Week / Older) are visible. |
| 3 | Inspect the API request(s) made for conversation data. Check `limit` and `offset` query params. | `limit` is ≤ 100. `offset` is present. No request uses `limit=1000`. |

## Expected Final State

`limit` is ≤ 100. `offset` is present. No request uses `limit=1000`.

## Pass/Fail Criteria

**Pass:**
- `limit` ≤ 10-100 in all conversation requests
- `offset` parameter present — pagination is active

**Fail:**
- Any request with `limit=1000` or no `limit` at all (https://next.elitea.ai/api/v2/elitea_core/folder/prompt_lib/5464?sort_by=created_at&sort_order=desc&limit=1000&offset=0
)
- `offset` is always absent or always 0
