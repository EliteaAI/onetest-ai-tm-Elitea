---
id: ELITEA-0075
title: "Text Filtering Narrows Autosuggest Results"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0075: Text Filtering Narrows Autosuggest Results

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that typing characters after `/` filters the autosuggest list to matching participant names.

**Coverage:** Live filtering by name; partial match; unmatched entries hidden

## Preconditions

- Agent with multiple participants of different names (e.g., "Ado_repo_M", "planner", "%%%%")

## Test Data

Filter string: Ado

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent Instructions field and type `/`. | Dropdown shows all valid participants. |
| 2 | Continue typing `Ado`. | Dropdown narrows to show only participants whose names contain "Ado". Others are hidden. |
| 3 | Delete the typed characters back to `/`. | Full list is restored. |

## Expected Final State

Full list is restored.

## Pass/Fail Criteria

PASS: List filters live as characters are typed; full list restored on delete
FAIL: List does not filter; all entries remain visible regardless of input
