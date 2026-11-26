---
id: ELITEA-4916
title: "Skill ZIP import previews the files and creates the skill; ZIPs without exactly one SKILL.md or too large are refused"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:export, feat:import-forking, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4916: Skill ZIP import previews the files and creates the skill; ZIPs without exactly one SKILL.md or too large are refused

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that importing a skill ZIP shows its files in the import preview and creates the skill with those files, whether `SKILL.md` is inside a folder or at the top of the ZIP, and that a ZIP without exactly one `SKILL.md`, or one that is too large, is refused with a reason and creates no skill.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- The ZIP files from Test Data are saved locally.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| P-folder | `qa-7185-pkg.zip`: `qa-7185-pkg/SKILL.md`, `qa-7185-pkg/references/format.md`, `qa-7185-pkg/scripts/count.py` |
| P-root | `qa-7185-root.zip`: the same files with `SKILL.md` at the top of the ZIP (skill name `qa-7185-root`) |
| Z0 | `qa-7185-noskill.zip`: `references/format.md` and `scripts/count.py`, no `SKILL.md` |
| Z2 | `qa-7185-twoskill.zip`: `a/SKILL.md` and `b/SKILL.md` |
| Z-big | A ZIP with a valid `SKILL.md` that is larger than the server limit (confirm the limit with the dev team) |

`SKILL.md` of P-folder:

~~~markdown
---
name: qa-7185-pkg
description: QA 7185 package skill. Use when the user asks for a QA-7185 report or to count words.
---
# QA 7185 package skill
For the answer format, read `references/format.md` and follow it exactly.
To count words in a text, run `scripts/count.py` with the text as argument and report its result.
~~~

`references/format.md`: "Start every answer with `REF-OK:` and end with `-- qa7185`." `scripts/count.py` prints `WORDS= <n>` for its arguments.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skills → **Add** → **Import from file** and choose P-folder | The **Import parameters** dialog shows PROJECT, MAIN ENTITY `qa-7185-pkg` ("Type: Skill \| Version: base"), DESCRIPTION, INSTRUCTIONS and **FILES (2):** `references/format.md`, `scripts/count.py` |
| 2 | Click **Import** | The skill page opens with **Files – 2**. The Files card shows "References 1 · Scripts 1" |
| 3 | Import P-root | Same preview and result as steps 1–2, for `qa-7185-root` |
| 4 | Import Z0, then Z2 | A toast says `Not supported file [<file>]: A skill ZIP must hold exactly one SKILL.md, at the root or inside one top-level folder; found 0` (`found 2` for Z2). No dialog opens and no skill is created |
| 5 | Import Z-big and click **Import** | An error toast says the skill is too large. The dialog stays open and no skill is created |

---

## Expected Final State

Two skills, `qa-7185-pkg` and `qa-7185-root`, exist with **Files – 2**. No skill is created from Z0, Z2 or Z-big. Keep `qa-7185-pkg` for ELITEA-4917 to ELITEA-4921; delete the other test skills after the run.

---

## Pass/Fail Criteria

**Pass:**
- Valid ZIPs create the skill with all their files.
- Each invalid ZIP shows its reason and creates nothing.

**Fail:**
- A file from the ZIP is missing in the preview or on the skill.
- An invalid ZIP creates a skill, or is refused without a reason.

---

## Notes

- Extends ELITEA-3749, ELITEA-2438 and ELITEA-4761 from `.md` to ZIP. The file picker also accepts `.skill` files (a ZIP with another extension).
- On dev (2026-11-26) step 5 failed: a 60 MB ZIP passed the preview, then the import request stayed pending for over 3 minutes and aborted with no message. No skill was created. The expected server message is "the skill is larger than a skill version can hold".
