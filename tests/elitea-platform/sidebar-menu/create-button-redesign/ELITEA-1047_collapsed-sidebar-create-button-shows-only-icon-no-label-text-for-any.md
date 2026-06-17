---
id: ELITEA-1047
title: "Collapsed Sidebar: Create Button Shows Only `+` Icon — No Label Text for Any Section"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1047: Collapsed Sidebar: Create Button Shows Only `+` Icon — No Label Text for Any Section

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in collapsed sidebar mode the Create button displays only the `+` icon with no label text, regardless of which section is active.

**Coverage:**
- Collapsed state for all main sections

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in collapsed state (click the `<` toggle to collapse)

## Test Data

All 8 main sections + Settings sub-sections

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse the sidebar using the `<` arrow toggle | Sidebar collapses; only icons are visible in the nav |
| 2 | Navigate to Chat (click the Chat icon) | Create button area shows only `+` icon — no text label |
| 3 | Navigate to Agents | Create button shows only `+` — no `Agent` text |
| 4 | Navigate to Pipelines | Create button shows only `+` — no `Pipeline` text |
| 5 | Navigate to Credentials | Create button shows only `+` — no `Credential` text |
| 6 | Navigate to Artifacts | Create button shows only `+` — no `Artifact Bucket` text |
| 7 | Navigate to Applications | Create button shows only `+` — no `Application` text |

## Expected Final State

Create button shows only `+` — no `Application` text

## Pass/Fail Criteria

**Pass:**
- Collapsed sidebar shows only `+` icon for every section — no entity name or \"Create\" text is visible

**Fail:**
- Any entity name text is visible alongside the `+` icon in collapsed mode
- Button layout breaks or label overflows in collapsed state
