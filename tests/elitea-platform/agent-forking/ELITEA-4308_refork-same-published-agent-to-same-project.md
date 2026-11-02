---
id: ELITEA-4308
title: "Re-fork same published agent to same project succeeds"
priority: critical
type: regression
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- First fork of a published agent to target project "testproj1" is complete (from ELITEA-4307)
- User has access to target project

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Same agent as first fork |
| Target Project | testproj1 (same project as first fork) |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog/Agent Hub | Catalog loads; published agents visible |
| 2 | Select the same published agent as first fork | Agent details displayed |
| 3 | Click the Fork button | Fork dialog appears |
| 4 | Select testproj1 (same target project) | Target project shown in dialog |
| 5 | Click Confirm button | Fork request submitted; HTTP 200 response received (NOT HTTP 400) |
| 6 | Wait for fork completion | Redirect to target project or success confirmation shown |
| 7 | Navigate to target project (testproj1) | Project loads; agents list shown |
| 8 | Verify two separate agents exist | Both forks visible in agent list |
| 9 | Verify agents have unique IDs | Both agents have different, distinct IDs |
| 10 | Open first forked agent and make a change (e.g., rename) | Change is applied to first agent only |
| 11 | Open second forked agent | Second agent remains unchanged; independent copy confirmed |
| 12 | Execute both agents | Both execute without errors |

## Expected Final State

- Two independent forked copies exist in target project
- Each fork has unique ID and separate metadata
- Changes to one fork do not affect the other
- Both forks are fully functional

## Pass/Fail Criteria

**Pass:**
- Second fork succeeds with HTTP 200 (NOT HTTP 400)
- Two separate agents now exist in target project
- Each fork has unique ID
- Forks are independent (changes to one don't affect other)
- Both forks are executable

**Fail:**
- Fork fails with HTTP 400 or other error
- Only one agent exists after second fork attempt
- Both agents have same ID
- Changes to one fork affect the other
- Either fork cannot be executed
