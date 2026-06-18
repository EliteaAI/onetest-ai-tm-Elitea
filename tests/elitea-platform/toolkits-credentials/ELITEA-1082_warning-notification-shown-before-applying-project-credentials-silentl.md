---
id: ELITEA-1082
title: "Warning/notification shown before applying project credentials silently (User A scenario)"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, issue:4392, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4392]
---
# ELITEA-1082: Warning/notification shown before applying project credentials silently (User A scenario)

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when User A (who does not have private credentials) opens a team toolkit with project credentials available, the system displays a notification/confirmation before silently applying project credentials.

**Coverage:**
- Notification shown before applying project credentials
- User A is informed about credential source (project vs private)
- User can confirm or cancel credential application
- No silent fallback to project credentials without user awareness

## Preconditions

- Two users exist: User A (no private credentials) and Admin/toolkit creator
- Team project toolkit exists with private credentials configured
- Project-level credentials with same name exist in the team project
- User A is authenticated and has access to the team project
- Browser: Chrome/Edge latest

## Test Data

- Team project toolkit with private credentials
- Project-level credentials with matching name
- User A: Team member without private credentials
- Toolkit URL in team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Admin: Create a toolkit in team project with private credentials configured | Toolkit is created with private credentials |
| 2 | Admin: Add project-level credentials with the same name to the team project | Project credentials are created |
| 3 | User A (without private credentials): Navigate to the team project and open the toolkit | Toolkit configuration page loads |
| 4 | Observe the behavior when User A opens the toolkit | Notification/confirmation is displayed stating that project credentials will be applied because private credentials are missing |
| 5 | Verify that User A can confirm or cancel the credential application | User has control over whether project credentials are applied |

## Expected Final State

User has control over whether project credentials are applied

## Pass/Fail Criteria

**Pass:**
- Notification/confirmation is displayed before applying project credentials
- User A is informed that project credentials will be used
- User can confirm or cancel the action
- No silent credential application without user knowledge

**Fail:**
- Project credentials are applied silently without notification
- User A is unaware that project credentials are being used
- No confirmation prompt is shown
- Credential source is ambiguous or hidden
