---
id: ELITEA-3602
title: "+ trigger still works for user mentions (regression)"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, eng:frontend, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

## Preconditions

- Team project conversation with 2 users and 1 private agent

## Test Data

| Users | "Alice", "Bob" |
| Private Agent | "Agent A" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Type `+` | Shows ONLY users (Alice, Bob), NO agents |
| 2 | Type `&` | Shows ONLY agent (Agent A), NO users |

## Pass/Fail Criteria

**Pass:** + shows only users, & shows only agents
**Fail:** + shows agents OR & shows users
