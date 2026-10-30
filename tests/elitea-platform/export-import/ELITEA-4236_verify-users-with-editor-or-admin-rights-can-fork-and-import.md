---
id: ELITEA-4236
title: "Verify users with Editor or Admin rights can fork and import with no error"
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
- User has a source project with an agent, a pipeline, a skill and a master agent with sub-agents
- User has a different target project where the role is Editor, and one where the role is Admin (or the role can be switched between runs)
- Export files are available: agent `.md`, agent `.zip`, pipeline `.md`/`.yaml`, skill export file

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

Fork combinations:

| Target role | Entity |
|-------------|--------|
| Editor | Agent |
| Editor | Pipeline |
| Editor | Skill |
| Editor | Master agent with sub-agents |
| Admin | Agent |
| Admin | Pipeline |
| Admin | Skill |
| Admin | Master agent with sub-agents |

Import combinations:

| Destination | Import file |
|-------------|-------------|
| Active project | agent `.md` |
| Active project | agent `.zip` |
| Active project | pipeline `.md`/`.yaml` |
| Active project | skill export file |
| Another project (Editor) | agent `.md` |
| Another project (Editor) | agent `.zip` |
| Another project (Editor) | pipeline `.md`/`.yaml` |
| Another project (Editor) | skill export file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the source project, open the entity from a Fork combinations row and start Fork | The Fork dialog opens |
| 2 | Select the target project where the user has the role from the row, and click Fork | The fork succeeds; no "Access denied" or error toast appears |
| 3 | Click the "Got it" link | The new forked entity opens in the target project |
| 4 | Check the forked entity details | "Forked from" is shown; sub-agents are present for the master agent |
| 5 | Repeat steps 1–4 for every Fork combinations row | Results match steps 1–4 |
| 6 | Open the entity list, click Import, select the file from an Import combinations row and select the destination | The [Import] button is enabled |
| 7 | Click [Import] | The import succeeds with no "Access denied" wording or error toast |
| 8 | Check the redirect | The user is redirected to the imported entity in the destination project |
| 9 | Repeat steps 6–8 for every Import combinations row | Results match steps 6–8 |

## Expected Final State

All fork and import operations by users with Editor or Admin rights in the target project succeed, with no "Access denied" message, correct "Got it" navigation, "Forked from" attribution and correct redirect after import.

## Pass/Fail Criteria

**Pass:**
- Every fork and import succeeds without any error toast or "Access denied" wording
- "Got it" opens the forked entity and "Forked from" is shown
- Import redirects to the imported entity

**Fail:**
- Any permitted fork or import is blocked or shows "Access denied"
- "Got it" does not open the new entity, or "Forked from" is missing
- Import does not redirect to the imported entity, or nested entities are missing
