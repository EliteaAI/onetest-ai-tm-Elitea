---
id: ELITEA-4639
title: "Only selected entity types are deleted; unselected types are preserved"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Project with non-zero counts for all seven entity types

## Test Data

| Selection Combination | Types Selected |
|---|---|
| Combination 1 | Chats, Credentials |
| Combination 2 | Agents, Toolkits |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record item counts for all seven types | Counts recorded |
| 2 | Select Combination 1 only, complete the typed-DELETE confirmation flow, and submit | Deletion completes |
| 3 | Recheck all seven counts | Chats and Credentials reduced as expected; Agents, Pipelines, Skills, Toolkits, MCPs unchanged |
| 4 | Re-seed test data, select Combination 2 only, and repeat the deletion flow | Deletion completes |
| 5 | Recheck all seven counts | Agents and Toolkits reduced; all other types unchanged |

## Expected Final State

In each run, only the explicitly selected types are reduced; every unselected type retains its exact prior count.

## Pass/Fail Criteria

**Pass:**
- Unselected types never change in either run

**Fail:**
- Any unselected type's count changes
