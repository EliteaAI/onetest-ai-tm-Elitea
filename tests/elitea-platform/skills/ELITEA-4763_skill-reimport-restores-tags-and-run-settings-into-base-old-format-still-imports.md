---
id: ELITEA-4763
title: "Skill re-import restores tags and run settings into a new base version; old-format and mixed files still import"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4763: Skill re-import restores tags and run settings into a new base version; old-format and mixed files still import

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that importing a skill export always creates a new skill with only a `base` version, restores tags and run settings from `metadata.elitea-*`, and that old-format and mixed-format export files still import.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `qa-export-check` from ELITEA-4762 exists, or any skill with tags and custom run settings.
- Files C and D from Test Data are saved locally as `.md` files.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Version `v2` settings | Another model, Custom max tokens 6000, a reasoning effort, Include project context on, extra tag `v2tag` |

File C (old format):

~~~yaml
---
name: legacy-skill
description: Old-format export
tags: [qa, legacy]
elitea_version: v2
elitea_run_settings:
  model: <valid model in the project>
  max_tokens: 2000
---
Legacy instructions.
~~~

File D (mixed):

~~~yaml
---
name: mixed-skill
description: Mixed-format export
tags: [old]
metadata:
  elitea-tags: '["new"]'
---
Mixed instructions.
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Round trip** | | |
| 1 | Open `qa-export-check`, change the settings to the `v2` values from Test Data and **Save As Version** `v2`. Export `v2` | The file contains `metadata.elitea-version: v2` and the `v2` settings |
| 2 | Import the exported file | A new skill is created with a new ID and only a `base` version, even though the file has `elitea-version: v2` |
| 3 | Check Tags and run settings of the imported skill | Tags, model, max tokens, reasoning effort and Include project context match version `v2` |
| 4 | Send a message in the skill Test panel | The response is generated with the restored model |
| **Old format** | | |
| 5 | Import file C | Import succeeds. Tags `qa` and `legacy`, the model and max tokens 2000 are restored. The version is `base` |
| 6 | Open the imported skill in **Edit** mode, then export it | The frontmatter and the export use `metadata.elitea-*`. There is no top-level `tags`, `elitea_version` or `elitea_run_settings` |
| **Mixed format** | | |
| 7 | Import file D | Import succeeds. The skill has the tag `new` (from `metadata.elitea-tags`), not `old` |

---

## Expected Final State

The imported skills have only a `base` version with tags and run settings restored. Delete the test skills after the run.

---

## Pass/Fail Criteria

**Pass:**
- Every import creates a new skill with only a `base` version.
- Tags and run settings are restored from the file.
- Old-format and mixed files import.

**Fail:**
- The imported skill has a non-base version, or tags or run settings are missing or wrong.
- An old-format or mixed file is rejected.
- Tags are taken from the top-level `tags` when `metadata.elitea-tags` is present.

---

## Notes

- Known bug #7622: the old-format import is rejected with `Unknown "elitea_run_settings" field(s): model`, and `metadata.elitea-tags` is rejected unless it is a valid JSON array string.
