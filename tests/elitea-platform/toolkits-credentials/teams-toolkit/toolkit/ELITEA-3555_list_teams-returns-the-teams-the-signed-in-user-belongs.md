---
id: ELITEA-3555
title: "list_teams — Returns the Teams the Signed-In User Belongs To"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3555: list_teams — Returns the Teams the Signed-In User Belongs To

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `list_teams` lists all joined teams, and that `name_contains` filters correctly.

## Preconditions

- Teams toolkit with `list_teams` enabled, linked to an authorized credential
- Test user is a member of at least two teams with distinguishable names

## Test Data

| Variant | name_contains | Expected |
|---|---|---|
| A | (omitted) | All joined teams returned |
| B | substring of one team's name | Only matching team(s) returned |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `list_teams` with no filter (Variant A) | Every team the test user is a member of is returned, each with id/displayName/description |
| 2 | Invoke `list_teams` with `name_contains` set per Variant B | Only teams whose name contains the substring are returned |

## Expected Final State

`list_teams` results accurately reflect team membership and filter correctly on name.

## Pass/Fail Criteria

**Pass:**
- Unfiltered call returns exactly the user's joined teams; filtered call returns only matches

**Fail:**
- Teams are missing/extra in the unfiltered result, or the filter returns non-matching teams
