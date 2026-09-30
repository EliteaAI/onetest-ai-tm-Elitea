---
id: ELITEA-3553
title: "& ESC key closes dropdown without inserting mention"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, eng:frontend, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation is open with private agent "CodeHelper"
- Chat message input field is visible and empty

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private Agent | "CodeHelper" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Type `&cod` | Private participant dropdown appears with filtered results |
| 2 | Press ESC | Dropdown closes; `&cod` remains as plain text |

## Pass/Fail Criteria

**Pass:** ESC closes dropdown without inserting mention
**Fail:** ESC doesn't close dropdown OR mention is inserted
