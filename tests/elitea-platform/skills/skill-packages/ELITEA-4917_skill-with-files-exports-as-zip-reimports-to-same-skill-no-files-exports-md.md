---
id: ELITEA-4917
title: "Skill with files exports as a ZIP that re-imports to the same skill; a skill without files still exports as .md"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:export, feat:import-forking, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4917: Skill with files exports as a ZIP that re-imports to the same skill; a skill without files still exports as .md

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that exporting a skill with files downloads a ZIP with the same files, that importing the download creates the same skill, and that a skill without files still exports as a single `.md` file.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `qa-7185-pkg` is imported from P-folder of ELITEA-4916 and shows **Files – 2**.
- Skill S-plain exists and shows **Files – 0**.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Skill with files | `qa-7185-pkg` (`references/format.md`, `scripts/count.py`) |
| Skill without files | S-plain (any skill with **Files – 0**) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On `qa-7185-pkg` open ⋮ → **Export** | `qa-7185-pkg.zip` downloads. It contains `qa-7185-pkg/SKILL.md`, `qa-7185-pkg/references/format.md` and `qa-7185-pkg/scripts/count.py` with unchanged content |
| 2 | Open Skills → **Add** → **Import from file**, choose the downloaded ZIP, then click **Import** | The preview shows **FILES (2)**. A new skill is created with the same name, description, instructions and **Files – 2** |
| 3 | On S-plain open ⋮ → **Export** | `<name>.md` downloads (not a ZIP), in the same format as ELITEA-4762 |

---

## Expected Final State

The re-imported skill matches `qa-7185-pkg`. Delete the re-imported skill after the run.

---

## Pass/Fail Criteria

**Pass:**
- The export and re-import keep every file and the skill content.
- A skill without files exports as `.md`.

**Fail:**
- The ZIP is missing a file, or a file content changes.
- The re-imported skill differs from the source.
- A skill without files exports as a ZIP.

---

## Notes

- A published version exports as `<name>.<version>.zip` (for example `ab-calc-skill.v2.zip`).
- Related: ELITEA-4762, ELITEA-4763.
