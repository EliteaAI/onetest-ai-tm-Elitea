---
id: ELITEA-3601
title: "# search still shows ALL agents including public (regression)"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, eng:frontend, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation is open with 1 private agent added
- Public agents exist in Agent Hub (not added to chat)

## Test Data

| Field | Value |
|-------|-------|
| Private agent in chat | "MyAgent" |
| Public agent NOT in chat | "PublicBot" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Type `#` | Dropdown shows ALL agents: "MyAgent" AND "PublicBot" |
| 2 | Type `&` | Dropdown shows ONLY "MyAgent" (private), NOT "PublicBot" |

## Pass/Fail Criteria

**Pass:** # shows ALL (private+public), & shows only private
**Fail:** # and & show identical lists
