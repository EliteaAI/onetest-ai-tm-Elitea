---
id: ELITEA-4636
title: "Delete Project Data section is visible only to authorized roles"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A private project exists with a designated owner and at least one non-owner member
- A team project exists with users assigned to Admin, Editor, and Viewer roles

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private project owner account | private-owner@test |
| Private project non-owner account | private-member@test |
| Team project Admin account | team-admin@test |
| Team project Editor account | team-editor@test |
| Team project Viewer account | team-viewer@test |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the private-project owner and navigate to Settings → General | "Delete Project Data" section is visible at the bottom of the page, below "Back Up & Restore" |
| 2 | Log in as a non-owner member of the same private project and navigate to Settings → General | "Delete Project Data" section is not visible/accessible |
| 3 | Log in as the team-project Admin and navigate to Settings → General | "Delete Project Data" section is visible |
| 4 | Log in as the team-project Editor and navigate to Settings → General | "Delete Project Data" section is not visible |
| 5 | Log in as the team-project Viewer and navigate to Settings → General | "Delete Project Data" section is not visible |

## Expected Final State

Only the private-project owner and team-project Admin can see and access the Delete Project Data section; Editor, Viewer, and non-owner private-project members cannot see it.

## Pass/Fail Criteria

**Pass:**
- Section visible only for owner (private) and Admin (team)
- Section hidden for Editor, Viewer, and non-owner member

**Fail:**
- Section visible to any unauthorized role
- Section hidden from an authorized role
