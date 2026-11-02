---
id: ELITEA-4309
title: "Fork same published agent multiple times to same project"
priority: critical
type: functional
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- Two forks of a published agent already exist in target project "testproj1" (from ELITEA-4307 and ELITEA-4308)

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Same agent as previous forks |
| Target Project | testproj1 |
| Fork Attempt Numbers | 3rd and 4th fork attempts |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog/Agent Hub | Catalog loads |
| 2 | Select same published agent | Agent details displayed |
| 3 | Click Fork button | Fork dialog appears |
| 4 | Select testproj1 | Target project shown |
| 5 | Click Confirm (third fork attempt) | HTTP 200 response (NOT HTTP 400) |
| 6 | Wait for completion | Third fork created successfully |
| 7 | Repeat steps 1-6 for fourth fork attempt | HTTP 200 response; fourth fork created |
| 8 | Navigate to testproj1 | Project agents list displayed |
| 9 | Verify all four forked agents appear | All four agents visible in list |
| 10 | Verify all have unique IDs | Each agent has distinct ID |
| 11 | Verify all are independently editable | Can edit each agent separately without affecting others |

## Expected Final State

- Four independent forked copies exist in target project
- Each fork has unique ID
- All forks are functional and independent

## Pass/Fail Criteria

**Pass:**
- Third and fourth forks both succeed with HTTP 200
- All four forks appear in target project with unique IDs
- No HTTP 400 or constraint violation errors

**Fail:**
- Third or fourth fork fails with HTTP 400
- HTTP 500 or internal error occurs
- Forks are missing from project list
- Multiple forks share same ID
