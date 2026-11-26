---
id: ELITEA-4922
title: "Skill ZIP package: import, export and re-import keep the files; invalid ZIP refused; files kept on Save As Version and fork"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:export, feat:import-forking, feat:fork, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4922: Skill ZIP package: import, export and re-import keep the files; invalid ZIP refused; files kept on Save As Version and fork

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify that a skill ZIP imports with its files, exports as a ZIP that re-imports to the same skill, is refused with a reason when it has no `SKILL.md`, and that Save As Version and fork keep the files.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in Project A and Project B.
- The ZIP files from Test Data are saved locally.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Package ZIP | `regression-skill-pkg.zip`: `regression-skill-pkg/SKILL.md`, `regression-skill-pkg/references/format.md`, `regression-skill-pkg/scripts/count.py` |
| Invalid ZIP | `regression-noskill.zip`: `references/format.md` only, no `SKILL.md` |
| Version name | `v2` |
| Target project | Project B |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skills → **Add** → **Import from file** and choose the package ZIP | **Import parameters** shows MAIN ENTITY `regression-skill-pkg` ("Type: Skill \| Version: base") and **FILES (2):** `references/format.md`, `scripts/count.py` |
| 2 | Click **Import** | The skill page opens with **Files – 2**. The Files card shows "References 1 · Scripts 1" |
| 3 | Import the invalid ZIP | Toast: `Not supported file [regression-noskill.zip]: A skill ZIP must hold exactly one SKILL.md, at the root or inside one top-level folder; found 0`. No dialog opens and no skill is created |
| 4 | On the imported skill open ⋮ → **Export** | `regression-skill-pkg.zip` downloads, containing `SKILL.md`, `references/format.md` and `scripts/count.py` |
| 5 | Import the downloaded ZIP and click **Import** | A second skill `regression-skill-pkg` is created with **Files – 2** and the same instructions |
| 6 | On the first skill click **Save As Version**, enter `v2` in **Create version**, click **Save** | Version `v2` opens with **Files – 2** |
| 7 | Open ⋮ → **Fork**, choose Project B in **Fork parameters**, click **Fork**, then **Got it** | **Fork Complete** lists the skill. The fork opens in Project B with **Files – 2** |

---

## Expected Final State

Three copies of the skill exist with the same two files. Delete the test skills in Project A and Project B after the run.

---

## Pass/Fail Criteria

**Pass:**
- Every copy has **Files – 2**.
- The invalid ZIP is refused with the reason and creates nothing.

**Fail:**
- A file is missing in any copy.
- The invalid ZIP creates a skill or shows no reason.

---

## Notes

**Source functional tests:** ELITEA-4916 (steps 1–2, 4), ELITEA-4917 (steps 1–2), ELITEA-4918 (steps 1, 4) — AC1–AC3 of EliteaAI/elitea_issues#7185
**Regression rationale:** The package round trip and the copy paths most likely to drop files.
**Selected checkpoints:** FILES list in the preview; Files count; refusal toast; export contents; re-import; Save As Version; fork.
**Not covered:** `SKILL.md` at the root of the ZIP, a ZIP with two `SKILL.md` files, the oversize ZIP (ELITEA-4916); publish and Discover (ELITEA-4918); `.md` export of a skill without files (ELITEA-3749).
