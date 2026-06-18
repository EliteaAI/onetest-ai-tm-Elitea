---
id: ELITEA-0014
title: "Exception Dropdown Shows Only Team and Private Projects"
priority: medium
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, guardrails, story:4434, filtering, r-2.0.2, admin, p2]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0014: Exception Dropdown Shows Only Team and Private Projects

**Module:** Agent Publishing Guardrails · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the project exception dropdown filters correctly and displays ONLY Team and Private projects, excluding Public projects from the list.

## Preconditions

Admin access to Guardrails
At least 1 Public project, 2 Team projects, and 2 Private projects exist in the environment

## Test Data

Public projects: PublicProject1
Team projects: TeamProject1, TeamProject2
Private projects: PrivateProject1, PrivateProject2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Enable "Block Agent Publishing" toggle (ON) | Toggle ON, dropdown appears |
| 3 | Click on the project exception dropdown | Dropdown opens with list of projects |
| 4 | Scroll through the entire project list in the dropdown | All available projects are visible |
| 5 | Verify TeamProject1 is present in the list | TeamProject1 is visible |
| 6 | Verify TeamProject2 is present in the list | TeamProject2 is visible |
| 7 | Verify PrivateProject1 is present in the list | PrivateProject1 is visible |
| 8 | Verify PrivateProject2 is present in the list | PrivateProject2 is visible |
| 9 | Search or scroll for PublicProject1 in the dropdown | PublicProject1 is NOT present in the list |
| 10 | Verify no Public projects appear in the dropdown | No projects with "Public" type are shown |
| 11 | Verify project type labels (if shown) indicate Team or Private only | Only "Team" or "Private" type labels appear |

## Expected Final State

Only "Team" or "Private" type labels appear

## Pass/Fail Criteria

PASS:
- All Team projects are present in the dropdown
- All Private projects are present in the dropdown
- NO Public projects appear in the dropdown
- Project type filtering is correct and consistent

FAIL:
- Any Team or Private project is missing from the dropdown
- Any Public project appears in the dropdown
- Project type filtering is incorrect or inconsistent
