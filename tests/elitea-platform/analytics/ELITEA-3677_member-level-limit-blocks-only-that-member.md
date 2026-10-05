---
id: ELITEA-3677
title: "Budget — Member-Level Limit Blocks Only That Member, Not the Whole Team Project"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, budget, team-project, enforcement, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6573]
---
# ELITEA-3677: Budget — Member-Level Limit Blocks Only That Member, Not the Whole Team Project

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that when one team member's individual budget limit is reached (while the overall team project limit still has room), only that member is blocked — other members of the same team project can still send messages normally.

**Coverage:**
- Member-level block applies only to the over-limit member
- Teammates under their own limit are unaffected

## Preconditions

- **Requires a team project with per-member limits configured, and one member already over their individual limit** (while the project-level limit still has room) — if no such setup is available, this case cannot be executed yet; flag with the environment/admin owner

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the over-limit member, send the test chat message in the team project | Request is blocked with a budget message |
| 2 | As a different member (under their own limit) of the same team project, send the test chat message | Request succeeds normally |

## Expected Final State

The member-level block is specific to the one member who is over their limit; teammates are unaffected.

## Pass/Fail Criteria

**Pass:**
- Over-limit member is blocked; other members are unaffected

**Fail:**
- Blocking one member also blocks the rest of the team project, or the over-limit member is not blocked at all
