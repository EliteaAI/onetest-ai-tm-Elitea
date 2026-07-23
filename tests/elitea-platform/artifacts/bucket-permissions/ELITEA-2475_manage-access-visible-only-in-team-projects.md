---
id: ELITEA-2475
title: "Manage Access Action Visible Only in Team Projects"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---
# ELITEA-2475: Manage Access Action Visible Only in Team Projects

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Manage access" action is available only in Team projects and not visible in Private or Public projects.

**Coverage:**
- AC1 from Story #5832: Feature is available only in Team projects
- AC1 from Story #5912: Manage access entry point remains restricted to Team projects

## Preconditions

- User is logged in to {{base_url}}
- User has access to at least one Team project, one Private project, and one Public project
- Each project has at least one bucket in Artifacts

## Test Data

- Team project with Admin or permission-manager role
- Private project with any role
- Public project with any role

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Team project | Project opens successfully |
| 2 | Go to Artifacts and select any bucket | Bucket content is displayed |
| 3 | Click three dots next to bucket name in sidebar | Context menu shows "Manage access" option |
| 4 | Navigate to a Private project | Project opens successfully |
| 5 | Go to Artifacts and select any bucket | Bucket content is displayed |
| 6 | Click three dots next to bucket name in sidebar | Context menu does NOT show "Manage access" option |
| 7 | Navigate to a Public project | Project opens successfully |
| 8 | Go to Artifacts and select any bucket | Bucket content is displayed |
| 9 | Click three dots next to bucket name in sidebar | Context menu does NOT show "Manage access" option |

## Expected Final State

"Manage access" action is visible only in Team projects; not available in Private or Public projects.

## Pass/Fail Criteria

**Pass:**
- Team project: "Manage access" context menu option are visible
- Private project: "Manage access" is not available (menu option absent)
- Public project: "Manage access" is not available (menu option absent)

**Fail:**
- "Manage access" appears in Private or Public projects
- "Manage access" is missing in Team project for authorized user
