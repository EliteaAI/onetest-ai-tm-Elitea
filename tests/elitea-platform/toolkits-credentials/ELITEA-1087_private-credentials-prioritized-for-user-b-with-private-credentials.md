---
id: ELITEA-1087
title: "Private credentials prioritized for User B with private credentials"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, issue:4392, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4392]
---
# ELITEA-1087: Private credentials prioritized for User B with private credentials

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when User B (who has private credentials) opens the same team toolkit, their private credentials are prioritized and applied instead of falling back to project credentials.

**Coverage:**
- Private credentials are prioritized over project credentials
- User B's credentials are correctly applied
- No silent fallback to project credentials when private credentials exist
- Credential precedence logic works correctly

## Preconditions

- Two users exist: User B (has private credentials) and Admin/toolkit creator
- Team project toolkit exists with private credentials configured
- Project-level credentials with same name exist in the team project
- User B has configured matching private credentials
- User B is authenticated and has access to the team project
- Browser: Chrome/Edge latest

## Test Data

- Team project toolkit with private credentials
- Project-level credentials with matching name
- User B: Team member WITH private credentials configured
- Toolkit URL in team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Admin: Create a toolkit in team project with private credentials configured | Toolkit is created with private credentials |
| 2 | Admin: Add project-level credentials with the same name to the team project | Project credentials are created |
| 3 | User B: Create matching private credentials in their Private workspace | User B's private credentials are created successfully |
| 4 | User B: Navigate to the team project and open the toolkit | Toolkit configuration page loads |
| 5 | Verify which credentials are applied in the toolkit configuration | User B's private credentials are applied (not project credentials); credential source is clearly indicated |
| 6 | Execute a toolkit tool to confirm credential usage | Tool executes using User B's private credentials (verify via audit logs or tool behavior) |

## Expected Final State

Tool executes using User B's private credentials (verify via audit logs or tool behavior)

## Pass/Fail Criteria

**Pass:**
- User B's private credentials are applied (not project credentials)
- Toolkit configuration shows private credentials are in use
- No fallback to project credentials occurs
- Credential precedence is correct: private > project

**Fail:**
- Project credentials are applied instead of User B's private credentials
- Silent credential switching occurs
- User B is not using their own credentials
- Credential source is ambiguous
