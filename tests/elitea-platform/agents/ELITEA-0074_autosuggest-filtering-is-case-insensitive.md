---
id: ELITEA-0074
title: "Autosuggest Filtering Is Case-Insensitive"
priority: high
type: functional
module: agents
status: deprecated
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0074: Autosuggest Filtering Is Case-Insensitive

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that autosuggest filtering matches participant names regardless of letter case.

**Coverage:** Lowercase, uppercase, and mixed-case inputs all match correctly

## Preconditions

- Agent with a toolkit named "Ado_repo_M" (mixed case)

## Test Data

Filter strings: /ado, /ADO, /Ado

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/ado` in Instructions. | "Ado_repo_M" appears in the dropdown. |
| 2 | Clear and type `/ADO`. | "Ado_repo_M" still appears. |
| 3 | Clear and type `/Ado`. | "Ado_repo_M" still appears. |

## Expected Final State

"Ado_repo_M" still appears.

## Pass/Fail Criteria

PASS: All three casing variants match the "Ado_repo_M" entry
FAIL: Any casing variant fails to match when the name clearly contains the substring
