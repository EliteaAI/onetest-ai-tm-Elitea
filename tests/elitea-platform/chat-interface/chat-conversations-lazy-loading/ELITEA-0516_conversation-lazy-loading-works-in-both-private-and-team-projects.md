---
id: ELITEA-0516
title: "Conversation Lazy Loading Works in Both Private and Team Projects"
priority: high
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4834]
---
# ELITEA-0516: Conversation Lazy Loading Works in Both Private and Team Projects

**Module:** Chat Conversations Lazy Loading · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversation lazy loading (paginated batch fetching on scroll) functions correctly in both a private project and a team project — confirming the feature is not limited to one project type.

**Coverage:**
- Initial batch loads and date groups render in a private project
- Scroll triggers next batch in a private project
- Initial batch loads and date groups render in a team project
- Scroll triggers next batch in a team project

## Preconditions

- Logged in to {{base_url}}
- Access to a private project with enough conversations to require scroll for more
- Access to a team project with enough conversations to require scroll for more
- DevTools → Network → Filter: `conversations`

## Test Data

- Private project: any personal project with 30+ conversations
- Team project: any shared team project with 30+ conversations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch to the private project. Navigate to Chat. Inspect the first conversation API request. | `limit`, `offset` present. Date groups render correctly for each conversation groups |
| 2 | Scroll to the bottom of any date group section in the private project. | A new batch request fires with incremented `offset`. New conversations append. |
| 3 | Switch to the team project. Navigate to Chat. Inspect the first conversation API request. | `limit`, `offset` present. Date groups render correctly for each conversation groups |
| 4 | Scroll to the bottom of any date group section in the team project. | A new batch request fires with incremented `offset`. New conversations append. |

## Expected Final State

A new batch request fires with incremented `offset`. New conversations append.

## Pass/Fail Criteria

**Pass:**
- Lazy loading (paginated batches on scroll) works identically in both private and team projects

**Fail:**
- Lazy loading works in one project type but not the other
- `limit=1000` appears in either project type
