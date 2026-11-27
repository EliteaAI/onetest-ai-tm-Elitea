---
id: ELITEA-4974
title: "Another user's Private project shows its own Project created"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** Each user's Private project shows that project's creation date; switching to a team project and back keeps the values correct.

## Preconditions

- **User B** has a Private project and is a member of team project **Team A**
- User A's Private project creation date is known (for comparison)

## Test Data

| Field | Value |
|-------|-------|
| Projects | User B Private, Team A |
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, open Settings → **General** on User B's Private project | Project created equals User B's Private `created_at`; differs from User A's Private project date |
| 2 | Switch to Team A | Project created equals Team A's `created_at` |
| 3 | Switch back to User B's Private project | Project created shows User B's Private value again |

## Expected Final State

Every project shows its own creation date for every user.

## Pass/Fail Criteria

**Pass:**
- Values match the API for each project and never leak from another user's project

**Fail:**
- User B's Private project shows another project's date, or a stale value after switching
