---
id: ELITEA-0076
title: "Escape Key Closes the Autosuggest Dropdown Without Inserting"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0076: Escape Key Closes the Autosuggest Dropdown Without Inserting

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that pressing Escape dismisses the autosuggest dropdown without inserting any text.

**Coverage:** Keyboard dismissal; no unintended text insertion

## Preconditions

- Agent with at least one configured participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into the Instructions field and type `/`. | Dropdown appears. |
| 2 | Press Escape. | Dropdown closes; cursor remains in Instructions field; no mention text is inserted. |
| 3 | Verify Instructions field content has only the `/` character (or original text + `/`). | No mention appended. |

## Expected Final State

No mention appended.

## Pass/Fail Criteria

PASS: Dropdown dismissed; no insertion; `/` remains as typed
FAIL: Dropdown remains visible; a mention is incorrectly inserted on Escape
