---
id: ELITEA-0678
title: "Fork Agent — Single Version is Forked to Target Project"
priority: critical
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0678: Fork Agent — Single Version is Forked to Target Project

**Module:** Fork · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that forking an agent from a specific version detail view copies only that version to the target project with `is_forked` set and a "Forked from" link visible.

**Coverage:**
- Single-version fork behaviour
- `is_forked` flag propagation for agents
- "Forked from" link rendering in Card and Table view
- Correct version isolation (not all versions)

## Preconditions

- Logged in as user with Editor role in Source Project and Editor role in Target Project
- Source Project contains an agent with at least 3 named versions
- Target Project exists and is accessible

## Test Data

- Source agent: any agent with ≥3 versions (e.g. "Testing Export")
- Active version during fork: Version 2 (non-latest)
- Target Project: any project other than Source (e.g. "Private")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents in Source Project → open the test agent → switch to Version 2 | Agent detail view shows Version 2 as active |
| 2 | Click the Fork icon (card header) or select Fork from ... menu | Fork/Import Wizard modal opens with title "Fork parameters" |
| 3 | Select Target Project from the dropdown | Target Project is selected; Fork button becomes active |
| 4 | Click Fork | Wizard shows progress then "Fork Complete" state |
| 5 | Navigate to Target Project → Agents → locate the forked agent | Agent is present in the list |
| 6 | Open the forked agent and check available versions | Exactly one version is present (Version 2 only) |
| 7 | Verify the agent card/row shows a "Forked from" link | "Forked from" link is visible in both Card View and Table View |
| 8 | Click the "Forked from" link | Browser navigates to the original agent in Source Project |

## Expected Final State

Browser navigates to the original agent in Source Project

## Pass/Fail Criteria

**Pass:**
- Only Version 2 is present in the forked agent
- "Forked from" link is visible and navigates correctly
- No crash or validation error occurs

**Fail:**
- All versions are copied instead of only the active one
- "Forked from" link is absent
- Fork completes but agent has 0 versions
