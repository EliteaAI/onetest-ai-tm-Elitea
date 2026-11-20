---
id: ELITEA-4764
title: "Skill editor frontmatter matches the export, syncs both ways with Tags and run settings, and rejects invalid values"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4764: Skill editor frontmatter matches the export, syncs both ways with Tags and run settings, and rejects invalid values

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the Instructions editor shows the same frontmatter as the export, that changes sync both ways between `metadata.elitea-*` and the Tags field and run settings, and that invalid values show an error while the form keeps its last valid value.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- A skill exists with a licence, the extra keys from file B of ELITEA-4761, tags and custom run settings.
- The skill has at least two versions with different settings.
- A reasoning model is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| New tag | `sync1` |
| Editor tags value | `elitea-tags: '["a", "b"]'` |
| Editor max tokens value | `elitea-max-tokens: "6000"` |
| Invalid values | `elitea-model: "not-a-model"`, `elitea-max-tokens: "abc"`, `elitea-tags: '[qa'` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Editor matches export** | | |
| 1 | Open the skill in Instructions **Edit** mode. Export the same version and compare the two frontmatter blocks | They are identical: key order (`name`, `description`, other stored keys, `metadata`), quoting and values |
| 2 | Create a new skill (do not save) | The frontmatter contains `metadata.elitea-model` with the project's default model |
| **Form → editor** | | |
| 3 | In the form, add tag `sync1`, change the model and set Custom max tokens | The `elitea-tags`, `elitea-model` and `elitea-max-tokens` lines update in the editor |
| **Editor → form** | | |
| 4 | In the editor, set `elitea-tags: '["a", "b"]'` and `elitea-max-tokens: "6000"` | The Tags field shows `a` and `b`. Max Completion Tokens shows Custom 6000 |
| 5 | In the editor, change `elitea-model` to a reasoning model | The model selector updates. The reasoning effort line and control match the new model |
| 6 | Delete the `elitea-max-tokens` line | Max Completion Tokens changes to Default |
| 7 | Type a half-finished value in a metadata line, for example `"60` in `elitea-max-tokens` | The cursor does not jump and the text is not rewritten while you type |
| **Invalid values** | | |
| 8 | Enter each invalid value from Test Data, one at a time | Each value shows an error under the editor. The form keeps its previous valid value |
| 9 | Fix the value through the form | The error clears and the line is rewritten with the form value |
| 10 | Enter an invalid value again, click **Save** and reload | The saved settings are the last valid form values, not the invalid text |
| 11 | Switch between the skill versions | The editor shows each version's own frontmatter |

---

## Expected Final State

The skill is saved with valid settings only. Delete any test skills created during the run.

---

## Pass/Fail Criteria

**Pass:**
- The editor frontmatter matches the export.
- Form and editor stay in sync both ways.
- Invalid values show an error and are never saved.

**Fail:**
- The editor and export differ.
- A change in one place does not appear in the other.
- An invalid value is saved, shows no error, or changes the form value.

---

## Notes

- Known bug #7635: `elitea-max-tokens` below the 4096 minimum for reasoning models is accepted in the editor.
