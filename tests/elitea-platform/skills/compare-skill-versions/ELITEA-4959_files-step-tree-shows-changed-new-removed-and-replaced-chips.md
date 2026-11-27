---
id: ELITEA-4959
title: "Files step tree shows Changed, New, Removed and Replaced chips, the summary line, Only changed and Not in <version>"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4959: Files step tree shows Changed, New, Removed and Replaced chips, the summary line, Only changed and Not in <version>

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify file statuses, the summary line, the Only changed switch, collapsible folders, the one-sided file layout and status recalculation while editing.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | Compare Files QA |
| Test data | `test-data/EL-7675/compare-files-qa/` (README lists every file and chip) |
| Expected summary | `4 changed · 1 new · 1 removed · 1 replaced` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open skill **Compare Files QA** → actions menu (⋮) → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare**. Click **Next**. | Files step opens; **Only changed** is ON. |
| 2 | Check the chips. | Changed: `references/guide.md`, `references/long.md`, `references/crlf.md`, `scripts/run.py`; New: `scripts/new-only.sh`; Removed: `assets/old-only.txt`; Replaced: `assets/logo.png`. `references/unchanged.md` and `references/nested/` are not listed. |
| 3 | Read the grey summary line. | `4 changed · 1 new · 1 removed · 1 replaced`. |
| 4 | Select `scripts/new-only.sh`, then `assets/old-only.txt`. | Missing side shows only grey `Not in base` / `Not in v2`; no field or buttons. Removed name is not struck through. |
| 5 | Turn **Only changed** OFF; expand `references/nested/deep`; select `references/unchanged.md`. | Unchanged files appear without a chip; folders collapse/expand; note `No differences in this file.` |
| 6 | Turn **Only changed** ON. | Unchanged files hide; the first visible file is selected. |
| 7 | Select `scripts/run.py`, change V2 text to `print("v1")` (do not save). | Changed chip disappears; summary shows `3 changed · …`. |
| 8 | Click **← Select versions**, confirm **Discard**, compare Base = `v2`, Compare with = `base`; open Files. | After the swap `new-only.sh` is **Removed** and `old-only.txt` is **New**; summary `4 changed · 1 new · 1 removed · 1 replaced`. |

---

## Expected Final State

No version data changed.

---

## Pass/Fail Criteria

**Pass:**
- Every chip and the summary match the test data README.
- Only changed and Not in <version> behave as designed; chips follow unsaved edits.

**Fail:**
- Any wrong chip or count.
- Unchanged files listed while Only changed is ON.
- Missing side shows a field or buttons.
