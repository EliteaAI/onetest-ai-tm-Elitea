---
id: ELITEA-1489
title: "FG13 - Get Team Projects (Happy Path)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_team_projects, teams, smoke, figma]
requirements: []
---
# ELITEA-1489: FG13 - Get Team Projects (Happy Path)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Verify get_team_projects retrieves all projects for a team, returning a list of projects with IDs and names.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_TEAM_ID env vars are set
Team has at least one project

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_TEAM_ID: valid Figma team ID with at least one project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_TEAM_ID to a valid team ID the user has access to | Environment variable set |
| 3 | Invoke get_team_projects tool with team_id parameter | API request sent to Figma team projects endpoint |
| 4 | Validate response contains projects array | Projects list present in response |
| 5 | Verify each project has id and name fields | Project metadata is complete |
| 6 | Confirm at least one project is returned | Team has accessible projects |

## Expected Final State

Team has accessible projects

## Pass/Fail Criteria

Projects array returned for the specified team
Each project has id and name fields
At least one project present
Tool completes without error
