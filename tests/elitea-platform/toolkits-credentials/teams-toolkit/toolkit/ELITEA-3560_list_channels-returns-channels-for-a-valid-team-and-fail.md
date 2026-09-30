---
id: ELITEA-3560
title: "list_channels — Returns Channels for a Valid Team and Fails Clearly for an Invalid One"
priority: critical
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3560: list_channels — Returns Channels for a Valid Team and Fails Clearly for an Invalid One

**Module:** Teams Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `list_channels` returns the channels of a specified team by ID or exact display name, and gives an actionable error otherwise.

## Preconditions

- Teams toolkit with `list_channels` enabled, linked to an authorized credential
- A known team with multiple channels

## Test Data

| Variant | team | Expected |
|---|---|---|
| A | exact team display name | Channels returned |
| B | team ID | Same channels returned |
| C | non-existent team name | Actionable error |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `list_channels` with Variant A | Channels are returned with id, displayName, description, membershipType, webUrl |
| 2 | Invoke `list_channels` with Variant B (the same team's ID) | Same set of channels is returned |
| 3 | Invoke `list_channels` with Variant C | Error explicitly points to `list_teams` to find the correct value |

## Expected Final State

Valid team lookups (by name or ID) return identical, complete channel lists; invalid lookups fail with actionable guidance.

## Pass/Fail Criteria

**Pass:**
- Name and ID lookups return the same complete channel set; invalid name fails with guidance to `list_teams`

**Fail:**
- Name and ID lookups diverge, required fields are missing, or the invalid-name error is generic
