---
id: ELITEA-4848
title: "Show more chat starters in the new-chat empty state for agents with 5 and 10 starters"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agents with 5 and 10 chat starters exist (starters numbered 1…K in the configured order)

## Test Data

| Agent | Collapsed | Link | Expanded |
|-------|-----------|------|----------|
| K = 5 | rows 1–4 | "Show 1 more" | 5 rows, "Show less" |
| K = 10 | rows 1–4 | "Show 6 more" | 10 rows, "Show less" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat → New chat and select the 5-starter agent | Rows 1–4 and the link "Show 1 more" |
| 2 | Click "Show 1 more", then "Show less" | All 5 rows in order and "Show less"; then back to 4 rows |
| 3 | Select the 10-starter agent | Rows 1–4 and "Show 6 more"; the link has `aria-expanded="false"` |
| 4 | Click "Show 6 more" | All 10 rows in configured order 1…10; "Show less"; `aria-expanded="true"`; row #10 is reachable |
| 5 | While expanded, click New chat and select the 10-starter agent again | The list starts collapsed (4 rows, "Show 6 more") |
| 6 | Expand, switch the participant to the 5-starter agent, then back | Each switch resets to collapsed (4 rows + "Show 1 more" / "Show 6 more") |

## Expected Final State

Every starter is reachable from the new-chat empty state. The expanded state never carries over to a new chat or a participant change.

## Pass/Fail Criteria

**Pass:**
- The collapsed state shows 4 rows plus the correct "Show N more"; expanding shows all K in order

**Fail:**
- Starters past the 4th can't be reached, the order differs, or the expanded state carries over
