---
id: ELITEA-4965
title: "Compare skill versions: Files step shows chips, summary, Only changed and file cards; step hidden when no version has files"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4965: Compare skill versions: Files step shows chips, summary, Only changed and file cards; step hidden when no version has files

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify the Files step of Compare versions for skills: the step order, the status chips and summary line, the Only changed switch, the one-sided and binary file layouts, and that the step is hidden when neither version has files.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `regression-compare-files` has draft versions `base` and `v2` with the files from Test Data (one folder per version, uploaded on the Files tab).
- Skill `regression-compare-nofiles` has 2 versions and no files.
- Neither skill has unsaved changes.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Changed (text, both versions) | `references/guide.md`, `references/long.md` (over 50,000 characters), `references/crlf.md`, `scripts/run.py` |
| New (only in v2) | `scripts/new-only.sh` |
| Removed (only in base) | `assets/old-only.txt` |
| Replaced (binary, different in each version) | `assets/logo.png` |
| Unchanged (identical in both) | `references/unchanged.md`, `references/nested/deep/same-nested.md`, `assets/same.png` |
| Expected summary | `4 changed · 1 new · 1 removed · 1 replaced` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `regression-compare-files` → ⋮ → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare** | **1. Instructions** with three step bars. The bottom bar has **← Select versions** on the left and **Next** on the right |
| 2 | Click **Next** | **2. Files** opens. **Only changed** is ON. The summary reads `4 changed · 1 new · 1 removed · 1 replaced` |
| 3 | Check the chips in the tree | **Changed**: guide.md, long.md, crlf.md, run.py. **New**: new-only.sh. **Removed**: old-only.txt. **Replaced**: logo.png. unchanged.md is not listed |
| 4 | Select `references/guide.md` | BASE and V2 columns show `references/guide.md`. Differing words are highlighted red on BASE and green on V2 |
| 5 | Select `scripts/new-only.sh` | The BASE side shows only `Not in base` |
| 6 | Select `assets/logo.png` | Each side shows a card with name, size and Download, framed in orange. No text field |
| 7 | Turn **Only changed** OFF | `references/unchanged.md` appears without a chip. The summary is unchanged |
| 8 | Click **Next** | **3. Run settings** opens with **Previous** and **Finish** |
| 9 | Click **Finish**. Open Compare versions on `regression-compare-nofiles`, click **Compare**, then **Next** | Two step bars. **Run settings** is step 2. No Files step |

---

## Expected Final State

No version data changed.

---

## Pass/Fail Criteria

**Pass:**
- Every chip and the summary match the Test Data.
- The Files step appears only when at least one version has files.

**Fail:**
- Any wrong chip or count.
- The Files step is missing, empty or out of order.
- A text editor is shown for a binary file.

---

## Notes

**Source functional tests:** ELITEA-4958, ELITEA-4959, ELITEA-4960
**Regression rationale:** The new Files step is the main change of EliteaAI/elitea_issues#7675; the checks are read-only, so the result is deterministic.
**Selected checkpoints:** step order and bottom bar; chips and summary; word highlights; Not in <version>; binary card; Only changed; step hidden without files.
**Not covered:** swapped versions, the over-limit card, chips updating while typing, the Viewer role.
