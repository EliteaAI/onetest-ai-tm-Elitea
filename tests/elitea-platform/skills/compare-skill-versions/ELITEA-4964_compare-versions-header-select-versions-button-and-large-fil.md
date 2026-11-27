---
id: ELITEA-4964
title: "Compare versions header, Select versions button and large file trees display correctly"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4964: Compare versions header, Select versions button and large file trees display correctly

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify visual details: version header meta in normal case with Save on the right, ← Select versions styling and hover, and layout with many files, deep folders and long names.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).
- Skill **Compare Many Files QA** has versions base and v2 uploaded from `compare-many-files-qa/` (30 changed files).
- One version of Compare Files QA has a name of 50+ characters.

---

## Test Data

| Field | Value |
|-------|-------|
| Long file name | `references/an-extremely-long-file-name-used-to-check-truncation-in-the-compare-files-tree-view.md` |
| Deep path | `references/a/b/c/file.md` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open skill **Compare Files QA** → actions menu (⋮) → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare**. | Header: version name, then date and author in normal case (e.g. `Jul 06, 2026, 10:13 · by Katsiaryna Yakauchyk`), left aligned, Save on the right. |
| 2 | Hover **← Select versions**. | Text button with a back arrow and no fill; grey fill on hover; same in light and dark theme. |
| 3 | Compare the 50+ character version name with base. | Name truncates or wraps without overlapping Save. |
| 4 | Compare **Compare Many Files QA** base vs v2 and open Files. | Summary `30 changed`; tree scrolls separately from the columns. |
| 5 | Expand `references/a/b/c`; select the long-name file. | Nested folders work; long name does not overlap the chip; column header shows the full path. |
| 6 | Click 10 files quickly. | The right side always shows the last clicked file; spinners clear. |

---

## Expected Final State

No version data changed.

---

## Pass/Fail Criteria

**Pass:**
- Header, button and tree layout match the design without overlap.

**Fail:**
- Meta in capitals, overlapping text, missing hover state or stale file content.
