---
id: ELITEA-1482
title: "FG14 - Get Team Projects (Invalid Team ID)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_team_projects, error-handling, negative, teams, figma]
requirements: []
---
# ELITEA-1482: FG14 - Get Team Projects (Invalid Team ID)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test get_team_projects error handling with an invalid team ID, verifying the tool returns an appropriate error message without crashing.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID env var is set
NEGATIVE test — team ID used is invalid or does not exist

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
Invalid team ID: "99999999999999" (non-existent team)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Prepare an invalid team ID (e.g., "99999999999999") | Invalid ID prepared for test |
| 3 | Invoke get_team_projects tool with the invalid team_id | API request sent with invalid team ID |
| 4 | Validate the response contains an error message (not found or forbidden) | Error message returned describing the failure |
| 5 | Confirm no Python exception or stack trace raised | Tool handles error gracefully |

## Expected Final State

Tool handles error gracefully

## Pass/Fail Criteria

Tool returns error message for invalid team ID
Error indicates team not found (404) or access denied (403)
No unhandled exception raised
Error message is descriptive
