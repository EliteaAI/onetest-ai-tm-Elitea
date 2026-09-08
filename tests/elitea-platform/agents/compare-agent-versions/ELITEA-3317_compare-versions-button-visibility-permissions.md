---
id: ELITEA-3317
title: "Compare Versions button displays only when Agent has 2+ versions and user has edit permissions"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Test Agents exist with different version counts
- Test user accounts with different permission levels (Edit, View-only)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Agent A | 1 version (base only) |
| Agent B | 2+ versions |
| User 1 | Edit permissions |
| User 2 | View-only permissions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User 1 (Edit permissions) and navigate to Agent A (base version only) | Compare Versions button is NOT visible |
| 2 | Navigate to Agent B (2+ versions) | Compare Versions button IS visible in the actions menu |
| 3 | Log out and log in as User 2 (View-only permissions) | Login successful |
| 4 | Navigate to Agent B (2+ versions) | Compare Versions button is NOT visible |
| 5 | Verify button is not accessible via keyboard navigation or direct URL manipulation | Button remains inaccessible for view-only user |

## Expected Final State

Compare Versions button is visible only when all conditions are met: Agent has 2+ versions AND user has edit permissions.

## Pass/Fail Criteria

**Pass:**
- Button hidden for Agents with only base version
- Button visible for Agents with 2+ versions when user has edit permissions
- Button hidden for view-only users regardless of version count

**Fail:**
- Button visible when it should be hidden
- Button hidden when it should be visible
- Button accessible to view-only users
