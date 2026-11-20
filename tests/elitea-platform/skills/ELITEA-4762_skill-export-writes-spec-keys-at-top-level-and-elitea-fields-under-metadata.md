---
id: ELITEA-4762
title: "Skill export writes only spec keys at the top level and ELITEA fields under metadata"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4762: Skill export writes only spec keys at the top level and ELITEA fields under metadata

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that exporting a skill created in ELITEA produces a file that follows the open Agent Skills spec: only spec keys at the top level, and ELITEA fields (tags, version, run settings) under `metadata` as flat `elitea-*` string values.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- A non-default model and a reasoning model with a reasoning effort setting are available in the project.
- Optional: the `skills-ref` validator CLI is installed (`skills-ref validate <file>`).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Name | qa-export-check |
| Description | Skill for export format check |
| Tags | `qa`, `export` |
| Model | Any fixed, non-default model (not Auto) |
| Max Completion Tokens | Custom, 5000 |
| Include project context | Off |
| Licence | `license: MIT` (added in the frontmatter editor) |
| Second version | `v2` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create the skill with the Test Data. In Instructions **Edit** mode, add `license: MIT` to the frontmatter. Click **Save** | The skill is saved |
| 2 | Export the `base` version | A `.md` file is downloaded |
| 3 | Check the top-level frontmatter keys | Only spec keys are present: `name`, `description`, `license`, `metadata` (plus `compatibility` / `allowed-tools` if set). There is no top-level `tags`, `version`, `elitea_version` or `elitea_run_settings` |
| 4 | Check the `metadata` block | Values are flat strings: `elitea-tags: '["qa", "export"]'` (JSON array string), `elitea-model: <selected model>`, `elitea-max-tokens: "5000"`, `elitea-ignore-project-context: "true"`. There is no `elitea-version` (the version is `base`) and no `elitea-model-selection` (the model is not Auto) |
| 5 | Optional: run `skills-ref validate` on the file | Validation passes |
| 6 | Set Max Completion Tokens to **Default**, save and export again | `elitea-max-tokens` is not in `metadata` |
| 7 | Turn **Include project context** on, save and export again | `elitea-ignore-project-context` is not in `metadata` |
| 8 | Select a reasoning model and a reasoning effort, save and export again | `metadata.elitea-reasoning-effort` contains the selected effort |
| 9 | Select **Auto** as the model, save and export again | `metadata.elitea-model-selection` is present |
| 10 | Save the skill as version `v2` and export `v2` | `metadata.elitea-version: v2` is present |

---

## Expected Final State

The exported files follow the spec layout. Delete the test skill after the run.

---

## Pass/Fail Criteria

**Pass:**
- The top level contains only spec keys.
- ELITEA fields are under `metadata` as flat strings and appear only when they apply.

**Fail:**
- Any of `tags`, `version`, `elitea_version` or `elitea_run_settings` is at the top level.
- A `metadata.elitea-*` value is not a string, has the wrong value, or is present when it should be omitted.

---

## Notes

- A skill imported with non-spec keys (for example `argument-hint`) is expected to fail `skills-ref validate`. This is by design and not covered here.
