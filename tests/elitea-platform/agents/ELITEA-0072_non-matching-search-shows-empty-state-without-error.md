---
id: ELITEA-0072
title: "Non-Matching Search Shows Empty State Without Error"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0072: Non-Matching Search Shows Empty State Without Error

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that typing `/` followed by text matching no participant shows an empty state or "No matching results" — no error, crash, or exception.

**Coverage:** Empty state for unmatched input; no error thrown; page remains stable

## Preconditions

- Agent with at least one configured participant

## Test Data

Search string: /xyzabc123

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into the Instructions field and type `/xyzabc123`. | Dropdown appears but shows no matching results (empty list or "No matching results" message). |
| 2 | Verify no error toast, console error, or crash occurs. | Page remains stable. |

## Expected Final State

Page remains stable.

## Pass/Fail Criteria

PASS: Empty state shown; page stable; no error
FAIL: Error message, crash, or exception occurs; dropdown does not open at all
