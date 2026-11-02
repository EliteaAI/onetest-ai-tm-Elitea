---
id: ELITEA-4235
title: "Verify Import into a project where user is Viewer is blocked with disabled [Import] button and nothing is created"
priority: critical
type: regression
module: fork-import
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is Editor in Team Project A and Viewer in Team Project B
- Export files are available: agent `.md`, agent `.zip` with nested dependencies, pipeline `.md`/`.yaml`, skill export file
- A second account with Editor or Admin rights in Team Project B is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Destination project | Team Project B (user role: Viewer) |
| Expected tooltip | "Insufficient permissions to import in this project." |

Combinations (run all steps once per row):

| Starting project | Entity | Import file |
|------------------|--------|-------------|
| Team Project A | Agent | agent `.md` |
| Team Project A | Agent with nested dependencies | agent `.zip` |
| Team Project A | Pipeline | pipeline `.md`/`.yaml` |
| Team Project A | Skill | skill export file |
| Team Project B | Agent | agent `.md` |
| Team Project B | Agent with nested dependencies | agent `.zip` |
| Team Project B | Pipeline | pipeline `.md`/`.yaml` |
| Team Project B | Skill | skill export file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the starting project from the Test Data row, go to the entity list and click Import | The Import dialog opens |
| 2 | Select the import file from the Test Data row | The file is accepted and its content is listed in the dialog |
| 3 | Select Team Project B as the destination | Project B is set as the destination |
| 4 | Check the [Import] button | [Import] is disabled and cannot be clicked |
| 5 | Hover the [Import] button | A tooltip reads "Insufficient permissions to import in this project." |
| 6 | Repeat steps 1–5 for every remaining row in the Test Data table | Results match steps 1–5 for every row |
| 7 | Log in with the second account (Editor/Admin in Project B) and check Agents, Pipelines and Skills in Project B | No entity from these import files exists in Project B |

## Expected Final State

Import into Project B is blocked for every entity type and file format, whether started from Project A or Project B; [Import] is disabled with the permission tooltip and nothing is imported.

## Pass/Fail Criteria

**Pass:**
- [Import] is disabled for every row with Project B as destination
- The tooltip text is exactly "Insufficient permissions to import in this project."
- Nothing is imported into Project B

**Fail:**
- [Import] is enabled or clickable for any row
- The tooltip is missing or has different wording
- Any entity is created in Project B
