---
id: ELITEA-0016
title: "Project Exception Dropdown Appears When Toggle Enabled"
priority: high
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, guardrails, story:4434, r-2.0.2, admin, ui, p1]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0016: Project Exception Dropdown Appears When Toggle Enabled

**Module:** Agent Publishing Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that when "Block Agent Publishing" toggle is set to ON, a multi-select dropdown appears for selecting exception projects, and it shows both Team and Private projects.

## Preconditions

Admin access to Guardrails configuration
Multiple test projects exist (at least 2 Team projects and 2 Private projects)

## Test Data

Project types expected in dropdown: Team and Private projects
Project types NOT expected: Public projects
Dropdown type: Multi-select (allows selecting multiple projects)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Locate "Block Agent Publishing" section with toggle in OFF state | Toggle is OFF, no dropdown visible |
| 3 | Click the toggle to switch it to ON | Toggle switches to ON state |
| 4 | Observe the UI for a project exception dropdown | Dropdown control appears below or next to the toggle |
| 5 | Click on the dropdown to view available projects | Dropdown opens, showing list of projects |
| 6 | Verify dropdown displays Team projects | At least one Team project is visible in the list |
| 7 | Verify dropdown displays Private projects | At least one Private project is visible in the list |
| 8 | Verify dropdown does NOT display Public projects | No Public projects are shown in the dropdown list |
| 9 | Select multiple projects from the dropdown (e.g., 2 Team, 1 Private) | Multiple projects can be selected simultaneously (checkboxes or multi-select behavior) |
| 10 | Verify selected projects are highlighted or checked in dropdown | Selected projects show visual indication (checkmark, highlight, chip) |
| 11 | Close the dropdown and verify selected projects are displayed | Selected project names appear as chips/tags or in a summary |
| 12 | Switch the toggle back to OFF | Toggle switches to OFF |
| 13 | Observe the project exception dropdown | Dropdown disappears or becomes hidden when toggle is OFF |

## Expected Final State

Dropdown disappears or becomes hidden when toggle is OFF

## Pass/Fail Criteria

PASS:
- Dropdown appears when toggle is switched to ON
- Dropdown shows both Team and Private projects
- Public projects are NOT shown in dropdown
- Multi-select functionality works (can select multiple projects)
- Selected projects are visually indicated
- Dropdown disappears when toggle is switched to OFF

FAIL:
- Dropdown does not appear when toggle is ON
- Dropdown is missing Team or Private projects
- Public projects appear in the dropdown
- Cannot select multiple projects (single-select only)
- Selected projects are not visually indicated
- Dropdown remains visible when toggle is OFF
