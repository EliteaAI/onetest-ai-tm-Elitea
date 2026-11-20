---
id: ELITEA-4765
title: "Skill names with -- are rejected on every entry point; descriptions accept any characters and warn over 1024"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4765: Skill names with -- are rejected on every entry point; descriptions accept any characters and warn over 1024

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that a skill name containing consecutive hyphens (`--`) is rejected on create, rename, import and Build with AI, and that a skill description accepts any characters and shows a warning (not an error) above 1024 characters.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Files E and F from Test Data are saved locally as `.md` files.
- Build with AI is available for skills.
- Optional: a skill whose name contains `--`, created before this rule was deployed.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Invalid names | `my--skill`, `a--b`, `data--cleaner` |
| Valid name | `my-skill` |
| Description of 1024 / 1025 characters | Any text of exactly 1024 / 1025 characters |

File E: a skill export with `name: my--skill`.

File F: a skill export with a description of 1025+ characters that contains `<`, `>`, `:`, quotes and non-ASCII characters (for example `Привет, «тест»`).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Name** | | |
| 1 | Create a skill named `my--skill` | A clear validation message is shown and Save is blocked |
| 2 | Rename an existing skill to `a--b` in the Name field, then in the frontmatter `name:` line | Both are rejected with the same clear message |
| 3 | Import file E | Import fails with a clear, user-readable message. No skill is created |
| 4 | In Build with AI, ask for a skill named `data--cleaner`. On the review step, set the name to `data--cleaner` | The generated name has no `--`. The manually entered name is rejected and Create is blocked |
| 5 | Optional: open the pre-existing `--` skill and edit any field | The name error is shown at once. Save is blocked until the skill is renamed |
| 6 | Create a skill named `my-skill` | The skill is saved |
| **Description** | | |
| 7 | Import file F | Import succeeds. The description keeps all special characters |
| 8 | Open the imported skill | A description length warning is shown. Save is still available |
| 9 | Enter a description of exactly 1024 characters, then 1025 characters, and save each time | No warning at 1024. A warning at 1025. The skill saves in both cases |
| 10 | Export the skill from step 7 and import the file again | The YAML is quoted correctly and the re-imported description is identical |

---

## Expected Final State

No skill with `--` in its name is created. Delete the test skills after the run.

---

## Pass/Fail Criteria

**Pass:**
- `--` names are rejected with a clear message everywhere.
- Descriptions with any characters are kept; over 1024 characters shows a warning but still saves.

**Fail:**
- A `--` name is accepted, or the error is technical or unclear.
- A description is changed, rejected, or blocked from saving because of its characters or a length between 1025 and the hard limit.

---

## Notes

- Known bug #7626: the import name error (step 3) shows a raw Pydantic message instead of a clear one.
- Build with AI keeps its own hard description limit (see ELITEA-1992).
