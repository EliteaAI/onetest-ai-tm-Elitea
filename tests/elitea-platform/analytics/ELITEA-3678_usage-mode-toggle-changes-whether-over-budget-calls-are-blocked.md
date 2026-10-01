---
id: ELITEA-3678
title: "Budget — Usage Mode Toggle Changes Whether Over-Budget Calls Are Blocked"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, budget, enforcement, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6573]
---
# ELITEA-3678: Budget — Usage Mode Toggle Changes Whether Over-Budget Calls Are Blocked

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that the admin-level budget enforcement setting is what actually controls whether an over-budget project gets blocked — with enforcement on, the call is blocked; with it off, the identical over-budget project can still be used normally.

**Coverage:**
- Enforcement off allows the over-budget call through
- Enforcement on blocks the identical over-budget call

## Preconditions

- **Requires admin access to the budget enforcement setting, and the same over-budget test project as ELITEA-3676** — if either is unavailable, this case cannot be executed yet; flag with the environment/admin owner

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As admin, turn budget enforcement OFF (or set to a non-enforcing mode) | Setting applied |
| 2 | As a member of the over-budget project, send the test chat message | Call completes successfully despite being over budget |
| 3 | As admin, turn budget enforcement back ON | Setting applied |
| 4 | Repeat the identical chat message in the identical over-budget project | Call is now blocked |

## Expected Final State

The same over-budget project behaves differently purely based on the enforcement setting — blocked when enforcement is on, allowed when it's off.

## Pass/Fail Criteria

**Pass:**
- Enforcement off → call succeeds; enforcement on → call is blocked, for the exact same over-budget project

**Fail:**
- Enforcement on fails to block, or enforcement off still blocks
