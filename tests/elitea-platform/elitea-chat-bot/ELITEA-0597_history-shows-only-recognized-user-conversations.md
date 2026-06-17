---
id: ELITEA-0597
title: "History shows only recognized user conversations"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0597: History shows only recognized user conversations

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the history panel contains only the current user's own recognizable sessions — no unknown, unresolved, or foreign entries.

**Coverage:**
- All listed sessions belong to and are recognizable by the current user
- No orphaned, unresolved, or unexpected entries in the list

## Preconditions

- Logged in on {{base_url}}
- At least 2 completed support sessions exist for this user

## Test Data

- Known session titles created by the test user (e.g., "How do I create an agent?", "Pipeline webhook configuration")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant widget | Widget opens |
| 2 | Click 'Chat history' (🕐) icon | History panel opens |
| 3 | Review all listed sessions | Every entry is recognizable as a session started by the current user — no unknown, blank-titled, or unresolved entries appear |

## Expected Final State

Every entry is recognizable as a session started by the current user — no unknown, blank-titled, or unresolved entries appear

## Pass/Fail Criteria

**Pass:**
- All history entries are recognizable conversations belonging to the current user

**Fail:**
- Any entry appears with an unrecognized title, blank label, or cannot be attributed to the current user's activity
