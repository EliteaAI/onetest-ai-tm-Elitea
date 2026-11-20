---
id: ELITEA-4761
title: "Skill import keeps license and non-ELITEA frontmatter keys, reports them, and exports them unchanged"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4761: Skill import keeps license and non-ELITEA frontmatter keys, reports them, and exports them unchanged

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that importing a skill keeps `license` and every other frontmatter key that ELITEA does not use (`compatibility`, `allowed-tools`, `argument-hint`, other tools' `metadata`), lists the unused keys in the import message, keeps them after save, and writes them back unchanged on export. `allowed-tools` must not pre-approve tools.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Files A and B from Test Data are saved locally as `.md` files.
- The real `pdf` skill (`SKILL.md`) from https://github.com/anthropics/skills is downloaded.
- An agent exists with at least one tool that requires approval before it runs.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Agent | Any agent with a tool that requires approval |

File A (`pdf-helper`):

~~~yaml
---
name: pdf-helper
description: Helps with PDFs
license: Apache-2.0
---
# PDF helper
Read the PDF and summarise it.
~~~

File B (`pdf-helper-extra`): file A with these extra keys:

~~~yaml
---
name: pdf-helper-extra
description: Helps with PDFs
license: Apache-2.0
compatibility: Requires Python 3.11
allowed-tools: Read Write
argument-hint: "[file]"
metadata:
  author: qa
  short-description: test
---
# PDF helper
Read the PDF and summarise it.
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **License (file A)** | | |
| 1 | Open Skills → **Import** and import file A | Import succeeds. The import message does not list `license` as unused |
| 2 | Open the imported skill and switch Instructions to **Edit** | The frontmatter shows `license: Apache-2.0` after `name` and `description` |
| 3 | Change one word in the body, click **Save**, then reload the page | The skill saves. `license: Apache-2.0` is still in the frontmatter |
| 4 | Export the `base` version and open the `.md` file | `license: Apache-2.0` is at the top level of the frontmatter |
| **Other keys (file B)** | | |
| 5 | Import file B | Import succeeds. The message reads "Skill imported. Kept but not used by ELITEA:" and lists `compatibility`, `allowed-tools`, `argument-hint` and the `metadata` keys, each once and readable |
| 6 | Open the imported skill in **Edit** mode | All extra keys are in the frontmatter with their original values. `argument-hint` is at the top level. `author` and `short-description` are under `metadata` |
| 7 | Export the skill and compare the file with file B | `compatibility`, `allowed-tools`, `argument-hint`, `metadata.author` and `metadata.short-description` are unchanged |
| 8 | Attach the skill to the agent from Preconditions. In chat, ask the agent to use the tool that requires approval | The approval prompt is shown. `allowed-tools` does not pre-approve the tool |
| **Real skill** | | |
| 9 | Import the anthropics `pdf` skill, then repeat steps 2 and 4 for it | Its `license` is kept in the frontmatter and written to the export |

---

## Expected Final State

The imported skills keep `license` and every extra frontmatter key through save and export. Delete the test skills after the run.

---

## Pass/Fail Criteria

**Pass:**
- `license` and all extra keys are kept after import, save and export, with their original values.
- The import message lists the unused keys.
- Tool approval still applies.

**Fail:**
- Any key is dropped, renamed, moved or changed.
- The import message is missing or lists keys incorrectly.
- A tool listed in `allowed-tools` runs without approval.

---

## Notes

- The licence is kept only in the frontmatter. No separate "License" form field is expected; record it if one is shown.
- Replaces the earlier behaviour where unrecognised keys were dropped (ELITEA-4280).
